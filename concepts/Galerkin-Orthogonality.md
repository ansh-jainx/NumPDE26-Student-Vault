---
tags: [chapter-3, Galerkin, orthogonality, best-approximation, exam-critical]
first_appears: "[[Week-03-FEM-I]]"
---

# Galerkin Orthogonality

**Reference:** §2.2 (first); reprised §3.1.3 in [[Week-05-Parametric-FEM-and-Error]]

---

## Statement

$$a(u - u_h, v_h) = 0 \qquad \forall v_h \in V_{h,0}$$

The Galerkin error $u - u_h$ is **$a$-orthogonal** to the discrete space $V_{h,0}$.

## Geometric Interpretation

$u_h$ is the $a$-orthogonal projection of $u$ onto $V_h$. In the energy norm:

$$\|u - u_h\|_a = \min_{v_h \in V_{h,0}} \|u - v_h\|_a$$

This is the **best approximation property**: the FEM solution is the closest element of $V_h$ to $u$ in the energy norm (for symmetric, coercive $a$).

> [!warning] Symmetric vs non-symmetric
> For symmetric $a$: best approximation is exact (no extra constant). For non-symmetric $a$: Galerkin orthogonality still holds, but best approximation only up to the factor $C_a/\alpha$ via [[Cea-Lemma]].

## Consequence

FEM error analysis reduces to **interpolation theory**: how well can $V_h$ approximate $u$? The PDE problem (existence/uniqueness) is separated from the approximation problem.

---

**Problems:** 3-15, 3-19 | **Related:** [[Galerkin-Discretization]], [[Cea-Lemma]], [[A-Priori-FEM-Error-Estimates]]
