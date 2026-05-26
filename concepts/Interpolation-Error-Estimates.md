---
tags: [chapter-3, interpolation, error-estimates, shape-regularity, exam-critical]
first_appears: "[[Week-06-Convergence-and-Accuracy]]"
---

# Interpolation Error Estimates

**Reference:** §3.3.1–§3.3.2, §3.3.5

---

## 1D Piecewise Linear Interpolation (§3.3.1)

On an interval of length $h$, for $u \in H^2$:

$$|u - I_h u|_{H^1} \leq h\,\|u''\|_{L^2}, \qquad \|u - I_h u\|_{L^2} \leq h^2\,\|u''\|_{L^2}$$

## 2D Linear Interpolation (Thm 3.3.2.21)

On a shape-regular triangulation $\mathcal{M}$ with mesh width $h_{\mathcal{M}}$, for $u \in H^2(\Omega)$:

$$|u - I_1 u|_{H^1(\Omega)} \leq C\,h_{\mathcal{M}}\,|u|_{H^2(\Omega)}$$

## Shape Regularity (Def 3.3.2.20)

$$\rho_{\mathcal{M}} = \max_K \frac{\mathrm{diam}(K)}{\mathrm{diam}(\text{inscribed circle of } K)}$$

> [!warning] Constant depends on shape regularity
> The constant $C$ in interpolation estimates depends on $\rho_{\mathcal{M}}$, not on $h$. Degenerate meshes (very flat triangles) blow up $C$.

## General Estimate (Thm 3.3.5.6)

For degree-$p$ Lagrangian FEM, $u \in H^k(\Omega)$, $0 \leq l \leq 1$:

$$\|u - I_p u\|_{H^l(\Omega)} \leq C\,h_{\mathcal{M}}^{\min(p+1,k)-l}\,|u|_{H^{\min(p+1,k)}(\Omega)}$$

> [!tip] The key formula for exams
> The exponent is $\min(p+1, k) - l$. The rate is limited by both the FEM degree ($p$) and the regularity of $u$ (Sobolev index $k$). Setting $l = 0$ gives $L^2$-error, $l = 1$ gives $H^1$-seminorm error.

---

**Problems:** 3-2, 3-5, 3-6, 3-15, 3-21 | **Related:** [[Cea-Lemma]], [[A-Priori-FEM-Error-Estimates]], [[Sobolev-Spaces]], [[Elliptic-Regularity]]
