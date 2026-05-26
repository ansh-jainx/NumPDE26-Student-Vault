---
tags: [formulas, chapter-1, Sobolev, norms, quick-reference]
---

# Quick Reference: Sobolev Norms & Inequalities

---

## Norms

| Norm | Formula | Space |
|------|---------|-------|
| $L^2$ norm | $\|u\|_0 = \left(\int_\Omega u^2\,\mathrm{d}\mathbf{x}\right)^{1/2}$ | $L^2(\Omega)$ |
| $H^1$ seminorm | $|u|_{H^1} = \|\nabla u\|_0 = \left(\int_\Omega |\nabla u|^2\,\mathrm{d}\mathbf{x}\right)^{1/2}$ | $H^1(\Omega)$ |
| $H^1$ norm | $\|u\|_{H^1} = \left(\|u\|_0^2 + |u|_{H^1}^2\right)^{1/2}$ | $H^1(\Omega)$ |
| Energy norm | $\|u\|_a = \sqrt{a(u,u)}$ | Depends on $a$ |

## Key Inequalities

**First Poincaré-Friedrichs (Thm 1.3.4.17):**

$$\|u\|_0 \leq \mathrm{diam}(\Omega)\,|u|_{H^1} \qquad \forall u \in H_0^1(\Omega)$$

**Second Poincaré-Friedrichs (Thm 1.8.0.20):**

$$\|u - \bar{u}\|_0 \leq C_\Omega\,|u|_{H^1} \qquad \forall u \in H^1(\Omega), \quad \bar{u} = \frac{1}{|\Omega|}\int_\Omega u$$

**Cauchy-Schwarz:**

$$\left|\int_\Omega u\,v\right| \leq \|u\|_0\,\|v\|_0$$

**Multiplicative trace inequality (Thm 1.9.0.10):**

$$\|u\|_{L^2(\partial\Omega)} \leq C\,\|u\|_0^{1/2}\,\|u\|_{H^1}^{1/2}$$

## Coercivity Recipes

| Setting | Bilinear form | Coercivity |
|---------|--------------|------------|
| Dirichlet on all $\partial\Omega$ | $a(u,v) = \int \nabla u \cdot \nabla v$ | $a(u,u) \geq C\,\|u\|_{H^1}^2$ on $H_0^1$ (Poincaré) |
| Mixed Dirichlet/Neumann | $a(u,v) = \int \kappa\nabla u \cdot \nabla v$ | Same, if $\Gamma_D \neq \emptyset$ |
| Robin ($c > 0$) | $a(u,v) = \int \nabla u \cdot \nabla v + c\int_{\partial\Omega} uv$ | Coercive on $H^1$ |
| Pure Neumann | $a(u,v) = \int \nabla u \cdot \nabla v$ | **Not** coercive on $H^1$ |

## Lax-Milgram Stability

$$\|u\| \leq \frac{C_\ell}{\alpha}$$

where $\alpha$ = coercivity constant, $C_\ell$ = continuity constant of $\ell$.
