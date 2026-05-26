---
tags: [chapter-3, convergence, h-refinement, p-refinement]
first_appears: "[[Week-05-Parametric-FEM-and-Error]]"
---

# Algebraic vs Exponential Convergence

**Reference:** §3.2.2 (Def 3.2.2.1)

---

## Algebraic Convergence (Def 3.2.2.1)

$$\text{error} = O(h^p) \quad \Leftrightarrow \quad O(N_{\text{DOF}}^{-p/d})$$

Straight line on a **log-log plot** with slope $p$ (the convergence rate).

## Exponential Convergence

$$\text{error} = O(e^{-\beta\,N^{\gamma}})$$

Curve **bends downward** on a log-log plot. Achieved by $p$-refinement on smooth solutions.

## When to Expect Each

| Setting | Convergence type | Rate |
|---------|-----------------|------|
| $h$-refinement, fixed $p$, smooth solution | Algebraic | $O(h^p)$ in $H^1$ |
| $h$-refinement, fixed $p$, corner singularity | Algebraic | $O(h^s)$ with $s < p$ |
| $p$-refinement, smooth solution | Exponential | $O(e^{-\beta\sqrt{N}})$ |
| $p$-refinement, singularity present | Algebraic only | Rate limited by regularity |

> [!tip] Exam skill
> Reading convergence from log-log plots: a straight line means algebraic convergence with rate = slope. Measure between two successive mesh levels.

---

**Problems:** 3-15, 3-19, 3-21 | **Related:** [[Lagrangian-FEM]], [[Elliptic-Regularity]], [[A-Priori-FEM-Error-Estimates]]
