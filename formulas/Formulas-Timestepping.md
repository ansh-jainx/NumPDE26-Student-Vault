---
tags: [formulas, chapter-9, timestepping, quick-reference]
---

# Timestepping Formulas — Quick Reference

---

## Heat Equation

$$\frac{\partial}{\partial t}(\rho u) - \operatorname{div}(\kappa\,\operatorname{grad}\,u) = f \quad \text{in } \Omega \times\, ]0,T[$$

## Spatial Variational Form

$$m(\dot{u}, v) + a(u, v) = \ell(t)(v) \quad \forall v \in V_0$$

| | Formula |
|---|---|
| $m(u,v)$ | $\int_\Omega \rho\,u\,v\,\mathrm{d}\mathbf{x}$ |
| $a(u,v)$ | $\int_\Omega \kappa\,\operatorname{grad}u \cdot \operatorname{grad}v\,\mathrm{d}\mathbf{x}$ |
| $\ell(t)(v)$ | $\int_\Omega f(\cdot,t)\,v\,\mathrm{d}\mathbf{x}$ |

## Energy Decay (Lemma 9.2.3.8)

$$\|u(t)\|_m \leq e^{-\gamma t}\|u_0\|_m \qquad (\gamma \text{ from Poincare-Friedrichs})$$

## Method-of-Lines ODE

$$\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}(t)$$

## Timestepping Schemes

| Scheme | Formula | Order |
|--------|---------|-------|
| Explicit Euler | $\mathbf{M}\boldsymbol{\mu}^{(j)} = (\mathbf{M} - \tau\mathbf{A})\boldsymbol{\mu}^{(j-1)} + \tau\boldsymbol{\varphi}(t_{j-1})$ | 1 |
| Implicit Euler | $(\mathbf{M}+\tau\mathbf{A})\boldsymbol{\mu}^{(j)} = \mathbf{M}\boldsymbol{\mu}^{(j-1)} + \tau\boldsymbol{\varphi}(t_j)$ | 1 |
| Crank-Nicolson | $(\mathbf{M}+\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j)} = (\mathbf{M}-\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j-1)} + \frac{\tau}{2}(\boldsymbol{\varphi}(t_j)+\boldsymbol{\varphi}(t_{j-1}))$ | 2 |

## Stability Constraint (Explicit Methods)

$$\tau < \frac{2}{\lambda_{\max}}, \qquad \lambda_{\max} = O(h_{\mathcal{M}}^{-2}) \implies \tau = O(h_{\mathcal{M}}^2)$$

## Total Error (Meta-Theorem 9.2.8.5)

$$\text{error} \leq C(h_{\mathcal{M}}^p + \tau^q)$$

Balanced refinement for error reduction $\rho$: reduce $h$ by $\rho^{1/p}$, reduce $\tau$ by $\rho^{1/q}$.
