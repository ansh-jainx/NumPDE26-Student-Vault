---
tags: [chapter-2, Galerkin, linear-system, sparse]
first_appears: "[[Week-03-FEM-I]]"
---

# Galerkin Matrix

**Reference:** §2.2

---

## Definition

Given basis $\{b_1^h, \ldots, b_N^h\}$ for $V_{h,0}$, the [[Galerkin-Discretization]] yields:

$$\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$$

| Matrix/vector | Entry | Name |
|---------------|-------|------|
| $(\mathbf{A})_{ij}$ | $a(b_j^h, b_i^h)$ | Stiffness matrix (or Galerkin matrix) |
| $(\boldsymbol{\varphi})_i$ | $\ell(b_i^h)$ | Load vector |

## Properties

- **Symmetric** if $a$ is symmetric (typical for elliptic BVPs)
- **Positive definite** if $a$ is coercive
- **Sparse** if basis functions have **local support** (FEM hat functions overlap only with neighbors)

> [!info] Sparsity pattern
> For degree-$p$ Lagrangian FEM on a mesh: $(\mathbf{A})_{ij} \neq 0$ only if $\operatorname{supp}(b_i^h) \cap \operatorname{supp}(b_j^h) \neq \emptyset$. In 2D with linear FEM: $\sim 7$ nonzeros per row (vertex + its neighbors).

## In LehrFEM++

Built by [[Assembly-Algorithm]]: `AssembleMatrixLocally(0, dofh, dofh, provider, A_COO)` fills a `lf::assemble::COOMatrix<double>`, then `A_COO.makeSparse()` gives the Eigen sparse matrix.

---

**Problems:** 2-6, 2-7 | **Related:** [[Assembly-Algorithm]], [[Stiffness-Parabolic]]
