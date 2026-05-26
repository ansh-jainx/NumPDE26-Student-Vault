---
tags: [chapter-9, convergence, error-estimates, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Fully Discrete Method of Lines: Convergence

**Reference:** §9.2.8

---

## Total Error (Meta-Theorem 9.2.8.5)

Degree-$p$ Lagrangian FEM + $L(\pi)$-stable RK of order $q$, uniform timestep $\tau$:

$$\left(\tau\sum_{j=1}^M \|u(\tau j) - u_h^{(j)}\|_{H^1}^2\right)^{1/2} \leq C(h^p + \tau^q)$$

**Total error = spatial error + temporal error.** Refining only one parameter while the other dominates is wasteful.

## Balanced Refinement (§9.2.8.8)

Error reduction by factor $\rho$: reduce $h$ by $\rho^{1/p}$, reduce $\tau$ by $\rho^{1/q}$.

> [!warning] Conditionally stable methods are wasteful (Rem. 9.2.8.10)
> Explicit methods with $\tau = O(h^2)$: stability forces smaller timesteps than accuracy needs whenever $1/q < 2/p$.
> Example: explicit RK45 ($q=5$) would need degree-10 FEM to balance — impractical.

## Experimental Evidence (Exp. 9.2.8.3)

Higher-order $L(\pi)$-stable methods achieve faster temporal convergence matching their order, until the spatial error floor.

---

The spatial error term $h^p$ is precisely the a priori FEM error bound from [[A-Priori-FEM-Error-Estimates]] (Thm 3.3.5.6 combined with [[Cea-Lemma]]).

---

**Problems:** 9-17, 9-20 | **Exams:** 2024 Endterm 0-1, 2025 Endterm 0-2 | **Related:** [[A-Priori-FEM-Error-Estimates]], [[Cea-Lemma]]
