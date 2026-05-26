---
tags: [chapter-1, variational, abstract-framework, exam-critical]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Linear Variational Problem

**Reference:** §1.4.1

---

## Definition (Def. 1.4.1.6)

Given:
- Trial space $V$ (affine subspace of a Hilbert space)
- Test space $V_0$ (linear subspace)
- Bilinear form $a: V \times V_0 \to \mathbb{R}$
- Linear form $\ell: V_0 \to \mathbb{R}$

Find $u \in V$ such that:

$$a(u,v) = \ell(v) \qquad \forall v \in V_0$$

## Trial vs Test Space

| Space | Role | Encodes |
|-------|------|---------|
| $V$ (trial) | Where $u$ lives | Inhomogeneous essential BCs ($u = g$ on $\Gamma_D$) |
| $V_0$ (test) | Where $v$ lives | Homogeneous essential BCs ($v = 0$ on $\Gamma_D$) |

> [!tip] Offset function technique (§1.4.1.9)
> For inhomogeneous Dirichlet: pick any $u_g \in V$ satisfying the BC. Set $u = u_0 + u_g$ with $u_0 \in V_0$. Solve the modified problem on $V_0$: $a(u_0, v) = \ell(v) - a(u_g, v)$.

## Equivalence with Minimization

By [[Quadratic-Minimization-Problem|Thm 1.4.1.8]]: if $a$ is s.p.d., then solving the variational problem is equivalent to minimizing $J(v) = \frac{1}{2}a(v,v) - \ell(v)$.

---

**Problems:** 1-6, 1-8, 1-10 | **Related:** [[Lax-Milgram-Theorem]], [[Galerkin-Discretization]], [[Spatial-Variational-Formulation-Parabolic]]
