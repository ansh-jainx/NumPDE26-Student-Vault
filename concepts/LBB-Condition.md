---
tags: [chapter-12, LBB, inf-sup, saddle-point, exam-critical]
first_appears: "[[Week-09-Stokes-I]]"
---

# LBB Condition (Inf-Sup)

**Reference:** Thm 12.2.2.23

---

## Ladyzhenskaya–Babuška–Brezzi (LBB)

For the saddle-point problem: find $(v, p) \in U \times Q$:

$$a(v, w) + b(w, p) = \ell(w) \;\forall w \in U, \qquad b(v, q) = 0 \;\forall q \in Q$$

**Theorem 12.2.2.23:** If

1. **(LBB1)** $a$ is coercive on $U$: $a(v,v) \geq \alpha \|v\|^2$
2. **(LBB2)** Inf-sup on $b$:
   $$\inf_{q \in Q} \sup_{v \in U} \frac{b(v,q)}{\|v\|_U \|q\|_Q} \geq \beta > 0$$

then there exists a **unique solution** with stability bound $\|(v,p)\| \leq C(\|\ell\| + \|g\|)$.

## Stokes incarnation

For Stokes: $U = (H_0^1)^d$, $Q = L^2(\Omega)$, $b(\mathbf{v},q) = -\int q\,\mathrm{div}\,\mathbf{v}$.

> [!warning] Discrete LBB (Week 10)
> The **continuous** inf-sup must be inherited by the **discrete** mixed spaces $(V_h, Q_h)$ for stable FEM. Equal-order $P_1$–$P_1$ violates discrete LBB → [[Pressure-Instability]].

## Intuition

LBB2 ensures pressure gradients can be "balanced" by velocity — prevents $p_h$ from being orthogonal to $\mathrm{div}\,V_h$.

---

**Problems:** 12-4 | **Related:** [[Stokes-Saddle-Point]], [[Taylor-Hood-FEM]], [[Formulas-Stokes]]
