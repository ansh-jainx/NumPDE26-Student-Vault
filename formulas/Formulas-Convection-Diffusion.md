---
tags: [formulas, chapter-10, convection-diffusion]
---

# Convection-Diffusion — Quick Reference

---

## Stationary BVP (§10.2.0.1)

$$-\varepsilon\,\Delta u + \mathbf{v} \cdot \nabla u = f \quad \text{in } \Omega, \qquad u = 0 \text{ on } \partial\Omega$$

## Weak form (no IBP on convection)

$$\varepsilon\int_\Omega \nabla u \cdot \nabla w + \int_\Omega (\mathbf{v} \cdot \nabla u)\,w = \int_\Omega f\,w \quad \forall w \in H_0^1(\Omega)$$

## Peclet number

$$\mathrm{Pe} = \frac{\|\mathbf{v}\|_{L^\infty}\,L}{\varepsilon}, \qquad L = \mathrm{diam}(\Omega)$$

## Inflow / outflow (§10.2.1.10–11)

$$\Gamma_{\mathrm{in}} = \{\mathbf{x} \in \partial\Omega : \mathbf{v} \cdot \mathbf{n} < 0\}, \qquad \Gamma_{\mathrm{out}} = \{\mathbf{x} : \mathbf{v} \cdot \mathbf{n} > 0\}$$

## Transient (§10.3.1)

$$\frac{\partial u}{\partial t} - \varepsilon\,\Delta u + \mathbf{v} \cdot \nabla u = f \quad \Rightarrow \quad \mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}(t)$$

## SUPG stabilization (§10.2.2.2)

Add to bilinear form: $\displaystyle \tau_K \int_K (\mathbf{v} \cdot \nabla u)\,(\mathbf{v} \cdot \nabla w)\,\mathrm{d}\mathbf{x}$

---

**Related:** [[Convection-Diffusion-Modeling]], [[Singular-Perturbation]], [[Upwind-Quadrature]], [[Streamline-Diffusion]], [[Week-08-Convection-Diffusion]]
