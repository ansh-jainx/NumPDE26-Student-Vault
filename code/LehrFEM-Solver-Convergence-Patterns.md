---
tags: [code, LehrFEM, solver, convergence, timestepping, validation]
---

# LehrFEM++ Solver & Convergence Patterns

---

## 1. Sparse Direct Solve

```cpp
Eigen::SparseMatrix<double> A = /* assembled + BCs applied */;
Eigen::VectorXd phi = /* load + BCs applied */;

// LU (general, non-symmetric)
Eigen::SparseLU<Eigen::SparseMatrix<double>> solver_lu;
solver_lu.compute(A);
Eigen::VectorXd mu_lu = solver_lu.solve(phi);

// LDL^T (symmetric positive definite — faster)
Eigen::SimplicialLDLT<Eigen::SparseMatrix<double>> solver_ldlt;
solver_ldlt.compute(A);
Eigen::VectorXd mu_ldlt = solver_ldlt.solve(phi);
```

---

## 2. Implicit Euler Timestepping

```cpp
// Pre-factorize system matrix (constant τ)
lf::assemble::COOMatrix<double> S_COO = M_COO;
S_COO.AddTo(tau, A_COO);
Eigen::VectorXd rhs_dummy = Eigen::VectorXd::Zero(S_COO.cols());
lf::assemble::FixFlaggedSolutionComponents<double>(selector, S_COO, rhs_dummy);
Eigen::SparseMatrix<double> S = S_COO.makeSparse();
Eigen::SparseLU<Eigen::SparseMatrix<double>> solver;
solver.compute(S);

Eigen::VectorXd mu = mu_0;  // initial condition
for (int j = 1; j <= M_steps; ++j) {
  double t_j = j * tau;
  // RHS = M * mu_old + tau * phi(t_j)
  Eigen::VectorXd rhs = M * mu + tau * phi(t_j);
  // Apply essential BC values to RHS consistently with selector
  for (unsigned int dof_idx = 0; dof_idx < rhs.size(); ++dof_idx) {
    auto [is_bd, val] = selector(dof_idx);
    if (is_bd) { rhs[dof_idx] = val; }
  }
  mu = solver.solve(rhs);
}
```

---

## 3. SDIRK-2 Timestepping

```cpp
// λ = 1 - 1/sqrt(2) (SDIRKMethodOfLines mastersolution notation)
const double lambda = 1.0 - 1.0 / std::sqrt(2.0);

// System matrix (same for both stages)
Eigen::SparseMatrix<double> S = M + lambda * tau * A;
Eigen::SparseLU<Eigen::SparseMatrix<double>> solver;
solver.compute(S);

Eigen::VectorXd mu = mu_0;
for (int j = 1; j <= M_steps; ++j) {
  // Homogeneous model as in SDIRKMethodOfLines mastersolution
  // Stage 1
  Eigen::VectorXd rhs = -A * mu;
  Eigen::VectorXd k1 = solver.solve(rhs);

  // Stage 2
  Eigen::VectorXd k2 = solver.solve(rhs - tau * (1.0 - lambda) * A * k1);

  // Update
  mu = mu + tau * ((1.0 - lambda) * k1 + lambda * k2);
}
```

> [!tip] SDIRK advantage
> Both stages use the same system matrix $\mathbf{M} + \lambda\tau\mathbf{A}$ — factorize once, solve twice per step.

---

## 4. Convergence Study (h-refinement)

```cpp
// Sequence of mesh levels
for (int level = 0; level < n_levels; ++level) {
  auto mesh_p = generate_mesh(level);  // progressively finer
  double h = mesh_width(mesh_p);

  // Solve
  Eigen::VectorXd mu = solve_on_mesh(mesh_p);

  // Compute errors against known exact solution
  auto mf_uh = lf::fe::MeshFunctionFE(fe_space, mu);
  auto mf_exact = lf::mesh::utils::MeshFunctionGlobal(u_exact);
  auto mf_err = mf_uh - mf_exact;

  // L2 norm of error
  double L2_err = std::sqrt(lf::fe::IntegrateMeshFunction(
      *mesh_p, lf::mesh::utils::squaredNorm(mf_err), 4));

  // H1 seminorm of error
  auto mf_grad_uh = lf::fe::MeshFunctionGradFE(fe_space, mu);
  auto mf_grad_exact = lf::mesh::utils::MeshFunctionGlobal(grad_u_exact);
  auto mf_grad_err = mf_grad_uh - mf_grad_exact;
  double H1_err = std::sqrt(lf::fe::IntegrateMeshFunction(
      *mesh_p, lf::mesh::utils::squaredNorm(mf_grad_err), 4));

  std::cout << h << " " << L2_err << " " << H1_err << std::endl;
}

// Check: log-log slope should match theoretical rate
// L2: slope ≈ p+1, H1: slope ≈ p (for smooth solution, convex domain)
```

---

## 5. Mesh Width Computation

```cpp
double mesh_width(std::shared_ptr<const lf::mesh::Mesh> mesh_p) {
  double h_max = 0.0;
  for (const lf::mesh::Entity* cell : mesh_p->Entities(0)) {
    double h_K = std::sqrt(lf::geometry::Volume(*cell->Geometry()));
    h_max = std::max(h_max, h_K);
  }
  return h_max;
}
```

---

## 6. Nodal Projection of Initial/Boundary Data

```cpp
// Project a function g onto the FE space (nodal interpolation)
auto mf_g = lf::mesh::utils::MeshFunctionGlobal(
    [](Eigen::Vector2d x) -> double { return g(x); });
Eigen::VectorXd mu_g = lf::fe::NodalProjection(*fe_space, mf_g);
```

---

## 7. Essential BC Selector Pattern

```cpp
auto bd_flags = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p);
auto selector = [&](unsigned int dof_idx) -> std::pair<bool, double> {
  const lf::mesh::Entity& node = dofh.Entity(dof_idx);
  if (bd_flags(node)) {
    Eigen::Vector2d x = lf::geometry::Corners(*node.Geometry()).col(0);
    return {true, g(x)};  // Dirichlet value
  }
  return {false, 0.0};
};
lf::assemble::FixFlaggedSolutionComponents<double>(selector, A_COO, phi);
```

---

## 8. Quadrature on Reference Element

```cpp
// Get quadrature rule for a triangle, exact for polynomials of degree ≤ 4
const lf::quad::QuadRule qr = lf::quad::make_QuadRule(lf::base::RefEl::kTria(), 4);
// qr.Points()  — 2 × n_pts matrix of reference coordinates
// qr.Weights() — n_pts vector of weights
// qr.NumPoints() — number of quadrature points

// Manual integration on cell K
double integral = 0.0;
auto pts = qr.Points();
auto wts = qr.Weights();
auto int_el = cell.Geometry()->IntegrationElement(pts);
for (int l = 0; l < qr.NumPoints(); ++l) {
  double f_val = /* evaluate f at mapped point */;
  integral += wts[l] * f_val * int_el[l];
}
```

---

**Related:** [[Method-of-Lines]], [[Timestepping-MOL]], [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]
