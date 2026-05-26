---
tags: [chapter-9, method-of-lines, Galerkin, semi-discrete, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Method of Lines (MOL)

**Reference:** §9.2.4

---

## Idea

Galerkin discretization in space only → ODE for expansion coefficients → timestepping.

## MOL ODE (Eq. 9.2.4.4)

Expand $u_h(t) = \sum_{i=1}^N \mu_i(t)\,b_i^h$ in the FE basis:

$$\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}(t), \qquad \boldsymbol{\mu}(0) = \boldsymbol{\mu}_0$$

| Matrix | Formula | Assembly in LehrFEM++ |
|--------|---------|----------------------|
| $\mathbf{A}$ (stiffness) | $a(b_j^h, b_i^h)$ | `ReactionDiffusionElementMatrixProvider` |
| $\mathbf{M}$ (mass) | $m(b_j^h, b_i^h)$ | `ReactionDiffusionElementMatrixProvider(fe_space, mf_zero, mf_rho)` |
| $\boldsymbol{\varphi}(t)$ (load) | $\ell(t)(b_i^h)$ | `ScalarLoadElementVectorProvider` |

> [!tip] Robin BCs
> Add boundary mass matrix contribution to $\mathbf{A}$ via `lf::uscalfe::MassEdgeMatrixProvider(fe_space, mf_c, bd_selector)` assembled with `AssembleMatrixLocally(1, dofh, dofh, edge_provider, A_COO)` (see Problem 9-2).

---

**Problems:** 9-1, 9-2, 9-20 | **Next:** [[Timestepping-MOL]], [[Stiffness-Parabolic]]
