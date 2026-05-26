---
tags: [chapter-1, existence-uniqueness, coercivity, exam-critical]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Lax-Milgram Theorem

**Reference:** §1.3.3, §1.4 (Thm 1.3.3.6: existence in Hilbert spaces; Thm 1.4.1.8: equivalence minimization ↔ variational problem)

> [!info] Naming
> The lecture notes do not use the name "Lax-Milgram." The existence/uniqueness result is Thm 1.3.3.6, and the minimization ↔ variational equivalence is Thm 1.4.1.8. The standard "Lax-Milgram" theorem from other references combines both.

---

## Statement (Thm 1.3.3.6 + Thm 1.4.1.8)

Let $V_0$ be a Hilbert space, $a: V_0 \times V_0 \to \mathbb{R}$ bilinear, $\ell: V_0 \to \mathbb{R}$ linear. If:

1. **Continuity:** $|a(u,v)| \leq C_a\,\|u\|\,\|v\|$ for all $u,v \in V_0$
2. **Coercivity:** $a(v,v) \geq \alpha\,\|v\|^2$ for all $v \in V_0$, with $\alpha > 0$
3. **Continuity of $\ell$:** $|\ell(v)| \leq C_\ell\,\|v\|$ for all $v \in V_0$

Then the [[Linear-Variational-Problem]] has a **unique solution** $u \in V_0$ satisfying:

$$\|u\| \leq \frac{C_\ell}{\alpha}$$

> [!warning] Coercivity is the hard condition
> - For $a(u,v) = \int_\Omega \nabla u \cdot \nabla v$ on $H_0^1$: coercivity follows from [[Sobolev-Spaces|Poincaré-Friedrichs]]
> - For $a(u,v) = \int_\Omega \nabla u \cdot \nabla v$ on $H^1$ (pure Neumann): **not coercive** (constants are in the kernel) — need compatibility condition on $\ell$
> - Robin BC: $a(u,v) = \int_\Omega \nabla u \cdot \nabla v + c\int_{\partial\Omega} uv$: coercive on $H^1$ if $c > 0$

## Role in FEM

Lax-Milgram on $V_0$ guarantees the continuous solution exists. Since $V_h \subset V_0$, the same theorem applied to $V_h$ guarantees the [[Galerkin-Discretization|Galerkin solution]] exists. The ratio $C_a/\alpha$ controls the condition number.

---

**Problems:** 1-6, 1-9, 1-10 | **Related:** [[Cea-Lemma]], [[Stability-Parabolic-Evolution]]
