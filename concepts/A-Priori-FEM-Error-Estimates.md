---
tags: [chapter-3, a-priori, error-estimates, convergence-rates, exam-critical]
first_appears: "[[Week-06-Convergence-and-Accuracy]]"
---

# A Priori FEM Error Estimates

**Reference:** §3.3.5 (Thm 3.3.5.6 combined with Céa's Lemma)

---

## The Chain

$$\underbrace{\text{Céa's Lemma}}_{\text{FEM error} \leq C \cdot \text{best approx}} \;+\; \underbrace{\text{Interpolation estimates}}_{\text{best approx} \leq C\,h^r\,|u|_{H^k}} \;=\; \text{a priori bound}$$

## Energy Norm ($H^1$-seminorm)

For degree-$p$ Lagrangian FEM on shape-regular mesh, $u \in H^k(\Omega)$:

$$|u - u_h|_{H^1(\Omega)} \leq C\,h_{\mathcal{M}}^{\min(p, k-1)}\,|u|_{H^{\min(p+1,k)}(\Omega)}$$

## $L^2$-Norm (via Aubin-Nitsche, §3.6.3)

If the domain is **2-regular** (convex polygon or smooth boundary):

$$\|u - u_h\|_{L^2(\Omega)} \leq C\,h_{\mathcal{M}}^{\min(p+1, k)}\,|u|_{H^{\min(p+1,k)}(\Omega)}$$

The $L^2$ error gains **one extra power of $h$** over the $H^1$ error.

## Convergence Rate Table

| FEM degree $p$ | Regularity $k$ | $H^1$ rate | $L^2$ rate | Typical scenario |
|:-:|:-:|:-:|:-:|---|
| 1 | 2 | $h$ | $h^2$ | Smooth solution, convex domain |
| 2 | 3 | $h^2$ | $h^3$ | Smooth, quadratic FEM |
| 1 | $1+s$ ($s < 1$) | $h^s$ | $h^{1+s}$ | Corner singularity |
| $p$ | $p+1$ | $h^p$ | $h^{p+1}$ | Optimal (smooth enough) |

> [!warning] Regularity is the bottleneck
> The rate is $\min(p, k-1)$ — limited by the weaker of FEM degree and solution regularity. On an L-shaped domain with $k \approx 5/3$, even degree-$p = 10$ FEM gives only $O(h^{2/3})$ in $H^1$ on uniform meshes. See [[Elliptic-Regularity]].

## Connection to Parabolic Problems

The spatial error term $h^p$ in [[Fully-Discrete-MOL-Convergence|Meta-Theorem 9.2.8.5]] (total error $\leq C(h^p + \tau^q)$) is precisely this a priori FEM error bound applied to the spatial Galerkin discretization.

---

**Problems:** 3-5, 3-6, 3-15, 3-19, 3-21 | **Related:** [[Cea-Lemma]], [[Interpolation-Error-Estimates]], [[Elliptic-Regularity]], [[Fully-Discrete-MOL-Convergence]]
