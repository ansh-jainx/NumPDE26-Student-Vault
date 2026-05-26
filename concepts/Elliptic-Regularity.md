---
tags: [chapter-3, regularity, Sobolev, corner-singularity]
first_appears: "[[Week-06-Convergence-and-Accuracy]]"
---

# Elliptic Regularity

**Reference:** §3.4

---

## The Question

Given $f \in L^2(\Omega)$, how smooth is the solution $u$ of $-\Delta u = f$? The Sobolev index $k$ in $u \in H^k(\Omega)$ determines the achievable FEM convergence rate via [[A-Priori-FEM-Error-Estimates]].

## Smooth Elliptic Lifting (Thm 3.4.0.2)

For smooth domains and coefficients: if $f$ is smooth, then $u$ is smooth. This is the ideal case but rarely applies to polygonal domains.

## Convex Domains (Thm 3.4.0.10)

For a **convex polygon** $\Omega$ with $f \in L^2(\Omega)$:

$$u \in H^2(\Omega), \qquad \|u\|_{H^2} \leq C\,\|f\|_{L^2}$$

This is **2-regularity** (or the "shift theorem"). It guarantees optimal $O(h)$ convergence for linear FEM in $H^1$.

## Non-Convex Domains: Corner Singularities

Re-entrant corner with interior angle $\omega > \pi$:

$$u \in H^{1+s}(\Omega), \qquad s = \frac{\pi}{\omega} < 1$$

> [!warning] The L-shaped domain — standard exam example
> L-shaped domain has $\omega = \frac{3\pi}{2}$, giving $s = \frac{2}{3}$. Linear FEM on uniform mesh: $O(h^{2/3})$ in $H^1$-seminorm instead of $O(h)$. The corner singularity dominates regardless of how smooth the data is.

## Impact on FEM

| Domain type | Regularity $k$ | Linear FEM $H^1$ rate | Linear FEM $L^2$ rate |
|:-:|:-:|:-:|:-:|
| Convex polygon | 2 | $h$ | $h^2$ |
| L-shaped ($\omega = 3\pi/2$) | $5/3$ | $h^{2/3}$ | $h^{5/3}$ |
| Slit domain ($\omega = 2\pi$) | $3/2$ | $h^{1/2}$ | $h^{3/2}$ |

---

**Problems:** 3-19 | **Related:** [[A-Priori-FEM-Error-Estimates]], [[Sobolev-Spaces]], [[Algebraic-vs-Exponential-Convergence]]
