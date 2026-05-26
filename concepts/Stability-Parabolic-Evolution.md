---
tags: [chapter-9, parabolic, stability, energy-decay, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Stability of Parabolic Evolution Problems

**Reference:** §9.2.3

---

## Main Result

> [!theorem] Lemma 9.2.3.8 — Exponential energy decay
> For $f \equiv 0$: $\|u(t)\|_m \leq e^{-\gamma t}\|u_0\|_m$ and $\|u(t)\|_a \leq e^{-\gamma t}\|u_0\|_a$
> where $\gamma > 0$ from Poincare-Friedrichs: $|v|_{H^1}^2 \geq \gamma\|v\|_{L^2}^2$.

**Physical meaning:** parabolic evolutions dissipate energy. Without forcing, solutions decay to zero.

## Proof Idea

Define $w(t) = e^{\gamma t}u(t)$, show $\frac{d}{dt}\|w\|_m^2 = 2m(\dot{w},w) = -2\tilde{a}(w,w) \leq 0$ using the product rule for bilinear forms and Poincare-Friedrichs.

## Convergence to Equilibrium

For time-independent $f$: $u(t)$ converges exponentially to the stationary solution $u^*$ of $a(u^*,v) = \ell(v)$.

---

**Problems:** 9-3 (discrete decay analogue) | **Related:** [[Stiffness-Parabolic]]
