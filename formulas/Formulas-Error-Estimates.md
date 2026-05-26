---
tags: [formulas, chapter-3, error-estimates, convergence, quick-reference]
---

# Quick Reference: FEM Error Estimates

---

## Céa's Lemma (Thm 3.1.3.7)

$$\|u - u_h\|_a \leq \frac{C_a}{\alpha}\,\inf_{v_h \in V_{h,0}} \|u - v_h\|_a$$

For symmetric $a$: $\|u - u_h\|_a = \inf_{v_h}\|u - v_h\|_a$ (exact best approximation).

---

## Interpolation Error Estimates

**1D linear (§3.3.1):**

$$|u - I_h u|_{H^1} \leq h\,\|u''\|_{L^2}, \qquad \|u - I_h u\|_{L^2} \leq h^2\,\|u''\|_{L^2}$$

**2D linear (Thm 3.3.2.21):**

$$|u - I_1 u|_{H^1(\Omega)} \leq C\,h_{\mathcal{M}}\,|u|_{H^2(\Omega)}$$

**General degree-$p$ (Thm 3.3.5.6):** for $u \in H^k(\Omega)$, $0 \leq l \leq 1$:

$$\|u - I_p u\|_{H^l(\Omega)} \leq C\,h_{\mathcal{M}}^{\min(p+1,k)-l}\,|u|_{H^{\min(p+1,k)}(\Omega)}$$

---

## A Priori FEM Error Bounds (Céa + Interpolation)

$$|u - u_h|_{H^1} \leq C\,h^{\min(p,\,k-1)}\,|u|_{H^k}, \qquad \|u - u_h\|_{L^2} \leq C\,h^{\min(p+1,\,k)}\,|u|_{H^k}$$

The $L^2$ bound requires 2-regularity of the dual problem (convex domain).

---

## Convergence Rate Table

| FEM degree $p$ | Regularity $k$ | $H^1$ rate | $L^2$ rate | Scenario |
|:-:|:-:|:-:|:-:|---|
| 1 | 2 | $h$ | $h^2$ | Smooth, convex domain |
| 2 | 3 | $h^2$ | $h^3$ | Smooth, quadratic FEM |
| 1 | $1+s$ ($s<1$) | $h^s$ | $h^{1+s}$ | Corner singularity |
| $p$ | $p+1$ | $h^p$ | $h^{p+1}$ | Optimal regularity |

---

## Strang's Second Lemma (§3.5)

When variational crimes are present ($a_h \neq a$):

$$\|u - u_h\| \leq C\!\left(\inf_{v_h}\|u - v_h\| + \sup_{w_h}\frac{|a(v_h,w_h) - a_h(v_h,w_h)|}{\|w_h\|} + \|\ell - \ell_h\|\right)$$

---

## Aubin-Nitsche Duality (§3.6)

**Output functional:** $|J(u) - J(u_h)| \leq \|u - u_h\|_a \cdot \|z - z_h\|_a$ where $z$ solves the dual problem $a(w,z) = J(w)$.

**$L^2$ estimate (§3.6.3):** $\|u - u_h\|_{L^2} \leq C\,h\,|u - u_h|_{H^1}$ (if 2-regular).

---

## Elliptic Regularity Quick Reference

| Domain | $u \in$ | Regularity $k$ |
|--------|---------|:-:|
| Convex polygon | $H^2(\Omega)$ | 2 |
| Re-entrant corner $\omega$ | $H^{1+\pi/\omega}(\Omega)$ | $1 + \pi/\omega$ |
| L-shaped ($\omega = 3\pi/2$) | $H^{5/3}(\Omega)$ | $5/3$ |
| Slit ($\omega = 2\pi$) | $H^{3/2}(\Omega)$ | $3/2$ |

---

## Shape Regularity (Def 3.3.2.20)

$$\rho_{\mathcal{M}} = \max_K \frac{\mathrm{diam}(K)}{\mathrm{diam}(\text{inscribed circle})}$$

All interpolation constants depend on $\rho_{\mathcal{M}}$, not on $h$. Bounded $\rho_{\mathcal{M}}$ means no degenerate triangles.

---

## Link to Parabolic Convergence

The $h^p$ term in [[Fully-Discrete-MOL-Convergence|Meta-Theorem 9.2.8.5]]:

$$\text{error} \leq C(h^p + \tau^q)$$

is precisely the a priori spatial FEM error bound from above.
