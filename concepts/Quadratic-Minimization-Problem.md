---
tags: [chapter-1, variational, minimization, exam-critical]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Quadratic Minimization Problem

**Reference:** §1.2.3, §1.3.2

---

## Definition (Def. 1.2.3.11)

Given a symmetric bilinear form $a: V \times V \to \mathbb{R}$ and a linear form $\ell: V \to \mathbb{R}$, find:

$$u^* = \arg\min_{v \in V} J(v), \qquad J(v) := \frac{1}{2}\,a(v,v) - \ell(v)$$

## Equivalence with Variational Problem (Thm 1.4.1.8)

If $a$ is **symmetric positive definite** (s.p.d.):

$$u^* = \arg\min J(v) \quad \Longleftrightarrow \quad a(u^*,v) = \ell(v) \;\;\forall v \in V_0$$

> [!tip] Why this equivalence matters
> - Minimization gives **physical intuition** (energy minimization)
> - Variational form gives **mathematical framework** (Lax-Milgram, Galerkin)
> - Both lead to the same solution — use whichever is more convenient

## Uniqueness (Thm 1.2.3.31)

If $a$ is positive definite ($a(v,v) > 0$ for $v \neq 0$), the minimizer is unique.

## Existence

- Finite dimensions: always exists (Thm 1.2.3.44)
- Infinite dimensions: need completeness of $V$ (Hilbert space) — see [[Sobolev-Spaces]]

---

**Problems:** 1-1, 1-5, 1-10 | **Related:** [[Linear-Variational-Problem]], [[Lax-Milgram-Theorem]]
