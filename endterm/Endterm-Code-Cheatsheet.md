---
tags: [endterm, exam-critical, code, LehrFEM]
---

# Endterm Code Cheatsheet

LehrFEM++ patterns for Ch.9 MOL/timestepping and Ch.12 Stokes — verified against NPDERepo mastersolutions. **2025 endterm was theory-only**; this sheet supports homework and **summer finals**.

Full references: [[LehrFEM-Solver-Convergence-Patterns]], [[LehrFEM-Stokes-Patterns]], [[LehrFEM-Assembly-Patterns]]

---

## Ch.9 — MOL assembly

### Mass and stiffness from bilinear forms

```cpp
// Stiffness A_ij = ∫ ∇b_i · ∇b_j  (κ=1, no zeroth-order term)
auto mf_one = [](const lf::mesh::Entity &e) { return 1.0; };
auto mf_zero = [](const lf::mesh::Entity &e) { return 0.0; };
lf::assemble::COOMatrix A_COO =
    lf::assemble::AssembleMatrixLocally<2, double>(
        *fe_space, 0,
        lf::uscalfe::ReactionDiffusionElementMatrixProvider(fe_space, mf_one, mf_zero));

// Mass M_ij = ∫ σ(x) b_i b_j  (weighted mass)
auto mf_sigma = /* coefficient σ(x) */;
lf::assemble::COOMatrix M_COO =
    lf::assemble::AssembleMatrixLocally<2, double>(
        *fe_space, 0,
        lf::uscalfe::ReactionDiffusionElementMatrixProvider(fe_space, mf_zero, mf_sigma));
```

**Repo folders:** `SDIRK` (NPDERepo name for HW/exam `MOLSDIRK`), `SDIRKMethodOfLines`, `ParabolicEvolutionAspects` (9-17 / 2024 Endterm — **not** in NPDERepo)

### Boundary mass (2024 Endterm / 9-17 style)

```cpp
// M_ij = ∫_{∂Ω} b_i b_j dS  — codim 1 assembly
lf::assemble::AssembleMatrixLocally<2, double>(*fe_space, 1, boundary_mass_provider);
```

### Robin BC edge contribution (9-2)

```cpp
// Adds c ∫_{∂Ω} u v dS to stiffness A — not M
// lf::uscalfe::MassEdgeMatrixProvider or lf::fe::MassEdgeMatrixProvider
lf::assemble::AssembleMatrixLocally<2, double>(*fe_space, 1, edge_robin_provider);
```

---

## Ch.9 — SDIRK-2 timestepping

**Butcher:** $\zeta = 1 - 1/\sqrt{2}$ (Ex. 9.2.7.49, `SDIRKMethodOfLines` / `SDIRK` mastersolutions)

```cpp
const double zeta = 1.0 - 1.0 / std::sqrt(2.0);
Eigen::SparseMatrix<double> S = M + zeta * tau * A;
Eigen::SparseLU<Eigen::SparseMatrix<double>> solver;
solver.compute(S);

// Stage 1: (M + ζτA) κ₁ = -τA μ + τφ(t + ζτ)
Eigen::VectorXd rhs1 = -tau * A * mu + tau * phi(t + zeta * tau);
Eigen::VectorXd kappa1 = solver.solve(rhs1);

// Stage 2: same S, RHS involves κ₁ (see mastersolution for exact combination)
Eigen::VectorXd kappa2 = solver.solve(/* stage-2 RHS */);

mu += /* b₁κ₁ + b₂κ₂ from Butcher tableau */;
```

> [!tip] Exam vs code
> Endterm asks for **symbolic** stage equations (Type D). Code: factorize **once**, solve **twice**.

---

## Ch.9 — Radau-3 (non-SDIRK)

**Repo:** `RadauThreeTimestepping`

```cpp
// Coupled 2N × 2N system — cannot reuse single N×N factorization for both stages
// Use Eigen::kroneckerProduct(I2, M) + tau * kron(A_butcher, A)
```

---

## Ch.9 — Essential BCs on MOL

```cpp
lf::assemble::FixFlaggedSolutionComponents<double>(selector, S_COO, rhs);
// Partition for time-dependent Dirichlet: identity block on boundary DOFs (9-11)
```

---

## Ch.12 — Taylor-Hood (summer final)

**Repo:** `StokesPipeFlow`, `TaylorHoodNonMonolithic`

```cpp
auto fe_space_u = std::make_shared<lf::uscalfe::FeSpaceLagrangeO2>(mesh_p);
auto fe_space_p = std::make_shared<lf::uscalfe::FeSpaceLagrangeO1>(mesh_p);
// Assemble A from viscous form, B from divergence, form block [A B^T; B 0]
// Pin one pressure DOF or enforce ∫ p_h = 0
```

See [[LehrFEM-Stokes-Patterns]] for block structure.

---

## Ch.12 — MINI / stabilized P1

| Folder | Element |
|--------|---------|
| `StokesMINIElement` | MINI bubbles |
| `StokesStabP1FEM` | equal-order + stabilization (`developers/`, not `homeworks/`) |

Endterm 2025 did **not** test these — summer finals 2024–2025 did.

---

## Summer final appendix

| Exam | Problem | Repo folder | HW |
|------|---------|-------------|-----|
| 2024 Summer | 1-3 Taylor-Hood | `TaylorHoodNonMonolithic` (exam folder; HW 12-3) | 12-1 pipe flow uses `StokesPipeFlow` |
| 2024 Winter | 1-3 MINI | `StokesMINIElement` | 12-2 |
| 2025 Summer | 1-2 Stabilized P1 | `StokesStabP1FEM` | 12-5 |

---

## Namespace note

Both `lf::fe::` and `lf::uscalfe::` appear in LehrFEM docs; NPDERepo mastersolutions mostly use `lf::uscalfe::` for scalar FE providers.

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Parabolic-Timestepping-Problems]] | [[Stokes-Problems]]
