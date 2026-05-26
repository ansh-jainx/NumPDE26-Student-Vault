---
tags: [chapter-2, boundary-conditions, elimination, LehrFEM, exam-critical]
first_appears: "[[Week-04-FEM-II]]"
---

# Essential BC Treatment in FEM

**Reference:** §2.7.6

---

## The Problem

After assembly, the system $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$ corresponds to the variational problem on $V_h$ (full space). For Dirichlet BCs $u = g$ on $\Gamma_D$, we need to enforce $\mu_i = g(\mathbf{a}_i)$ for all DOFs $i$ on $\Gamma_D$.

## Approach: Row/Column Modification

1. **Flag** boundary DOFs: identify DOF indices $i$ where $\mathbf{a}_i \in \Gamma_D$
2. **Set** prescribed values: $\mu_i = g(\mathbf{a}_i)$
3. **Modify** the system: for each flagged DOF $i$:
   - Set row $i$ of $\mathbf{A}$ to $\mathbf{e}_i^T$ (unit row)
   - Set $\boldsymbol{\varphi}_i = g(\mathbf{a}_i)$
   - Subtract column $i$ contributions from RHS (to preserve symmetry)

## LehrFEM++

| Function | Variant |
|----------|---------|
| `lf::assemble::FixFlaggedSolutionComponents(selector, A_COO, phi)` | Modifies `lf::assemble::COOMatrix<double>` and RHS in-place, preserves symmetry |
| `lf::assemble::FixFlaggedSolutionCompAlt()` | Alternative: sets unit rows for flagged DOFs without zeroing off-diagonal columns (does **not** preserve symmetry) |

**Flagging boundary DOFs:**
```cpp
auto bd_flags = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p);
// Then create selector function that returns {true, g(x)} for boundary DOFs
```

> [!warning] Order matters
> Always assemble the full system first, then apply essential BCs. Applying BCs during assembly leads to errors if shared DOFs appear in multiple elements.

---

**Problems:** 2-10, 2-14 | **Related:** [[Boundary-Conditions-Elliptic]], [[Essential-vs-Natural-BCs]], [[Method-of-Lines]]
