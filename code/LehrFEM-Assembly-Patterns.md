---
tags: [code, LehrFEM, assembly, element-providers, patterns]
---

# LehrFEM++ Assembly Patterns

---

## 1. Full Assembly Pipeline

```cpp
// 1. Mesh
auto mesh_p = lf::mesh::test_utils::GenerateHybrid2DTestMesh(0);
// or: auto mesh_factory = std::make_unique<lf::mesh::hybrid2d::MeshFactory>(2);
// or: auto mesh_p = lf::io::GmshReader(std::move(mesh_factory), "mesh.msh").mesh();

// 2. FE space
auto fe_space = std::make_shared<lf::uscalfe::FeSpaceLagrangeO1<double>>(mesh_p);
// quadratic: FeSpaceLagrangeO2

// 3. DOF handler
const lf::assemble::DofHandler& dofh = fe_space->LocGlobMap();
const int N_dofs = dofh.NumDofs();

// 4. Stiffness matrix A
lf::assemble::COOMatrix<double> A_COO(N_dofs, N_dofs);
lf::uscalfe::ReactionDiffusionElementMatrixProvider provider(fe_space, mf_alpha, mf_zero);
lf::assemble::AssembleMatrixLocally(0, dofh, dofh, provider, A_COO);

// 5. Load vector phi
Eigen::VectorXd phi(N_dofs);
phi.setZero();
lf::uscalfe::ScalarLoadElementVectorProvider load_provider(fe_space, mf_f);
lf::assemble::AssembleVectorLocally(0, dofh, load_provider, phi);

// 6. Robin/Neumann boundary terms (optional)
// Both namespaces are valid in LehrFEM++ docs; NPDERepo mastersolutions mostly use uscalfe:
lf::uscalfe::MassEdgeMatrixProvider edge_provider(fe_space, mf_c, bd_selector);
lf::assemble::AssembleMatrixLocally(1, dofh, dofh, edge_provider, A_COO);

// 7. Essential BCs (must be applied on COOMatrix)
auto bd_flags = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p);
auto selector = [&](unsigned int dof_idx) -> std::pair<bool, double> {
    // Return {true, g_value} for Dirichlet DOFs, {false, 0} otherwise
};
lf::assemble::FixFlaggedSolutionComponents<double>(selector, A_COO, phi);

// 8. Convert to Eigen sparse
Eigen::SparseMatrix<double> A = A_COO.makeSparse();

// 9. Solve
Eigen::SparseLU<Eigen::SparseMatrix<double>> solver;
solver.compute(A);
Eigen::VectorXd mu = solver.solve(phi);
```

---

## 2. Element Matrix Provider (Custom)

```cpp
class MyElementMatrixProvider {
public:
  bool isActive(const lf::mesh::Entity& cell) const { return true; }
  Eigen::MatrixXd Eval(const lf::mesh::Entity& cell) const {
    const lf::geometry::Geometry* geo_p = cell.Geometry();
    // Get reference element
    const lf::base::RefEl ref_el = cell.RefEl();
    // Number of local shape functions
    const int n_loc = ref_el.NumNodes(); // for p=1
    // Compute element matrix...
    Eigen::MatrixXd elem_mat(n_loc, n_loc);
    // ...
    return elem_mat;
  }
};
```

---

## 3. Element Vector Provider (Custom)

```cpp
class MyElementVectorProvider {
public:
  bool isActive(const lf::mesh::Entity& cell) const { return true; }
  Eigen::VectorXd Eval(const lf::mesh::Entity& cell) const {
    const int n_loc = cell.RefEl().NumNodes();
    Eigen::VectorXd elem_vec(n_loc);
    // ...
    return elem_vec;
  }
};
```

---

## 4. Built-In Providers Quick Reference

| Provider | Computes | Arguments |
|----------|----------|-----------|
| `ReactionDiffusionElementMatrixProvider` | $\int_K \alpha\nabla b_i \cdot \nabla b_j + \gamma\,b_i\,b_j$ | `(fe_space, mf_alpha, mf_gamma)` |
| `ScalarLoadElementVectorProvider` | $\int_K f\,b_i$ | `(fe_space, mf_f)` |
| `lf::uscalfe::MassEdgeMatrixProvider` (also `lf::fe::MassEdgeMatrixProvider`) | $\int_e c\,b_i\,b_j\,\mathrm{d}S$ | `(fe_space, mf_c, bd_selector)` |
| `lf::uscalfe::ScalarLoadEdgeVectorProvider` (also `lf::fe::ScalarLoadEdgeVectorProvider`) | $\int_e g\,b_i\,\mathrm{d}S$ | `(fe_space, mf_g, bd_selector)` |

**MeshFunction wrappers:**
```cpp
auto mf_one   = lf::mesh::utils::MeshFunctionConstant(1.0);
auto mf_zero  = lf::mesh::utils::MeshFunctionConstant(0.0);
auto mf_f     = lf::mesh::utils::MeshFunctionGlobal(
    [](Eigen::Vector2d x) -> double { return f(x); });
```

---

## 5. Assembly Codim Convention

| `AssembleMatrixLocally(codim, ...)` | Loops over |
|-------------------------------------|-----------|
| `codim = 0` | Cells (triangles/quads) — stiffness, mass, load |
| `codim = 1` | Edges — boundary integrals (Robin, Neumann) |

---

## 6. COOMatrix → Sparse

```cpp
lf::assemble::COOMatrix<double> A_COO(N, N);
// ... assemble into A_COO ...
Eigen::SparseMatrix<double> A = A_COO.makeSparse();
```

> [!warning] COOMatrix allows duplicate entries
> Multiple contributions to the same $(i,j)$ are summed automatically when converting to sparse. This is exactly what cell-oriented assembly relies on.

---

**Related:** [[Assembly-Algorithm]], [[Galerkin-Matrix]], [[Essential-BC-Treatment]]
