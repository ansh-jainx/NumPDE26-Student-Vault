---
tags: [chapter-2, assembly, LehrFEM, cell-oriented, exam-critical]
first_appears: "[[Week-04-FEM-II]]"
---

# Assembly Algorithm

**Reference:** §2.7.4

---

## Cell-Oriented Assembly (Code 2.7.4.20/23)

```
A = sparse zero matrix (N × N)
for each cell K in mesh:
    A_K = element_matrix(K)           // local 3×3 (linear) or 6×6 (quadratic)
    for i = 1..n_local, j = 1..n_local:
        I = global_dof(K, i)          // DOF handler
        J = global_dof(K, j)
        A[I,J] += A_K[i,j]           // scatter-add
```

Same pattern for load vector: $\boldsymbol{\varphi}[I] \mathrel{+}= \boldsymbol{\varphi}_K[i]$.

## LehrFEM++ API

| Function | Role |
|----------|------|
| `lf::assemble::AssembleMatrixLocally(codim, dofh, dofh, provider, A_COO)` | Assemble stiffness/mass matrix |
| `lf::assemble::AssembleVectorLocally(codim, dofh, provider, phi)` | Assemble load vector |

**Element matrix providers:**

| Provider | Assembles |
|----------|-----------|
| `ReactionDiffusionElementMatrixProvider` | $\int_K \kappa\,\nabla b_i \cdot \nabla b_j + \int_K c\,b_i\,b_j$ |
| `MassEdgeMatrixProvider` | $\int_e c\,b_i\,b_j\,\mathrm{d}S$ (boundary edge mass, codim 1) |
| `ScalarLoadElementVectorProvider` | $\int_K f\,b_i\,\mathrm{d}\mathbf{x}$ |

> [!tip] Same pattern in Ch9
> The [[Method-of-Lines]] ODE uses the same assembly: $\mathbf{M}$ (mass) and $\mathbf{A}$ (stiffness) are assembled with exactly these providers. Robin BCs add an edge mass matrix to $\mathbf{A}$ via `MassEdgeMatrixProvider`.

---

**Problems:** 2-6, 2-7, 2-8, 2-14 | **Exams:** Midterm 0-2 appears in multiple years with varying formulations | **Related:** [[Local-Computations]], [[Galerkin-Matrix]], [[Method-of-Lines]]
