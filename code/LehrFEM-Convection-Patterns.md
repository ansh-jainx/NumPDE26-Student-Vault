---
tags: [code, LehrFEM, convection, upwind, SUPG]
---

# LehrFEM++ Convection Patterns

---

## 1. Convection Bilinear Form Provider

From Problem **2-17** — non-symmetric element matrix for $\int_K (\mathbf{v} \cdot \nabla u)\,w$:

```cpp
// Custom provider or use course ConvBLFMatrixProvider
class ConvBLFMatrixProvider {
public:
  bool isActive(const lf::mesh::Entity& cell) const { return true; }
  Eigen::MatrixXd Eval(const lf::mesh::Entity& cell) const {
    // For constant v on triangle K:
    // (C_K)_{ij} = |K| * (v · ∇λ_j) * λ̄_i  with λ̄_i = 1/3
    // Returns NON-SYMMETRIC n_loc × n_loc matrix
  }
};

lf::assemble::AssembleMatrixLocally(0, dofh, dofh, provider, A_COO);
```

> [!warning] Non-symmetric
> Use solvers that handle non-symmetric systems (`Eigen::SparseLU`, not SimplicialLDLT).

## 2. Full Convection-Diffusion Assembly

```cpp
// Diffusion (stiffness)
auto diff_provider = lf::uscalfe::ReactionDiffusionElementMatrixProvider(
    fe_space, mf_eps, mf_zero);
lf::assemble::AssembleMatrixLocally(0, dofh, dofh, diff_provider, A_COO);

// Convection (add to same matrix)
auto conv_provider = ConvBLFMatrixProvider(fe_space, mf_velocity);
lf::assemble::AssembleMatrixLocally(0, dofh, dofh, conv_provider, A_COO);
```

## 3. Transient MOL (Week 8 + Week 7)

Same pattern as [[LehrFEM-Solver-Convergence-Patterns]]: assemble $\mathbf{M}$, $\mathbf{A}$ (diffusion + convection), then implicit Euler / SDIRK.

## 4. Upwind / SUPG

- **Upwind quadrature:** modify quadrature points to upstream nodes per §10.2.2.1 — see Problems 10-2, 10-8
- **SUPG:** add stabilization term via extra element provider or modified bilinear form (10-6, 10-7)

---

**Related:** [[LehrFEM-Assembly-Patterns]], [[Upwind-Quadrature]], [[Streamline-Diffusion]], [[FEM-Assembly-Implementation-Problems]]
