---
tags: [chapter-2, Galerkin, discretization, exam-critical]
first_appears: "[[Week-03-FEM-I]]"
---

# Galerkin Discretization

**Reference:** §2.2

---

## Idea

Replace the infinite-dimensional space $V_0$ in the [[Linear-Variational-Problem]] with a finite-dimensional subspace $V_{h,0} \subset V_0$:

$$\text{Find } u_h \in V_h: \quad a(u_h, v_h) = \ell(v_h) \quad \forall v_h \in V_{h,0}$$

## Existence & Uniqueness (Thm 2.2.1.5)

Since $V_{h,0} \subset V_0$ is a (finite-dimensional) Hilbert space, [[Lax-Milgram-Theorem]] applies directly → unique Galerkin solution exists.

## Galerkin Orthogonality

$$a(u - u_h, v_h) = 0 \qquad \forall v_h \in V_{h,0}$$

The error $u - u_h$ is **orthogonal** to $V_{h,0}$ in the $a$-inner product → $u_h$ is the **best approximation** to $u$ from $V_{h,0}$ in the energy norm:

$$\|u - u_h\|_a = \min_{v_h \in V_{h,0}} \|u - v_h\|_a$$

> [!tip] Implication for FEM
> Galerkin error = best approximation error. To reduce the error, make $V_{h,0}$ larger (finer mesh or higher polynomial degree). The error analysis reduces to **interpolation theory** → see [[Cea-Lemma]].

## From Variational Problem to Linear System

Choose basis $\{b_1^h, \ldots, b_N^h\}$ for $V_{h,0}$, expand $u_h = \sum_j \mu_j\,b_j^h$ → [[Galerkin-Matrix|linear system]] $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$.

---

**Problems:** 2-1, 2-2, 2-14 | **Related:** [[Galerkin-Orthogonality]], [[Galerkin-Matrix]], [[Linear-FEM-1D]], [[Method-of-Lines]]
