---
tags: [chapter-2, FEM, Lagrangian, polynomial-degree, p-refinement]
first_appears: "[[Week-04-FEM-II]]"
---

# Lagrangian Finite Elements

**Reference:** §2.5–§2.6

---

## Finite Element Triple (§2.5)

A finite element is $(K, P_K, \Sigma_K)$:

| Component | Meaning |
|-----------|---------|
| $K$ | Element geometry (triangle, quadrilateral, ...) |
| $P_K$ | Local polynomial space (e.g., $\mathcal{P}_p$ = polynomials of degree $\leq p$) |
| $\Sigma_K$ | Set of DOFs (linear functionals that uniquely determine $u \in P_K$) |

**Unisolvence:** $\Sigma_K$ must uniquely determine every $u \in P_K$ — equivalent to the interpolation matrix being invertible.

## Lagrangian FEM

DOFs = **point evaluations** at specific nodes. The global FE space:

$$\mathcal{S}_p^0(\mathcal{M}) = \{u \in C^0(\overline{\Omega}) : u|_K \in \mathcal{P}_p(K) \;\forall K \in \mathcal{M}\}$$

| Degree $p$ | Nodes per triangle | Basis functions |
|------------|-------------------|----------------|
| 1 | 3 (vertices) | Barycentric coords $\lambda_i$ |
| 2 | 6 (vertices + edge midpoints) | $\lambda_i(2\lambda_i - 1)$, $4\lambda_i\lambda_j$ |
| 3 | 10 (vertices + 2 per edge + 1 interior) | ... |

## $h$- vs $p$-Refinement

- **$h$-refinement:** fix $p$, make mesh finer → [[Algebraic-vs-Exponential-Convergence|algebraic convergence]] $O(h^p)$
- **$p$-refinement:** fix mesh, increase $p$ → [[Algebraic-vs-Exponential-Convergence|exponential convergence]] for smooth solutions

> [!info] LehrFEM++
> `lf::uscalfe::FeSpaceLagrangeO1` (linear), `lf::uscalfe::FeSpaceLagrangeO2` (quadratic). Problems 9-17 and 9-20 use $S_2^0(\mathcal{M})$.

---

**Problems:** 2-4, 2-12 | **Related:** [[Triangular-Linear-FEM-2D]], [[Parametric-FEM]]
