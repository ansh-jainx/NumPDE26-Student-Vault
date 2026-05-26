---
tags: [chapter-1, modeling, elliptic, electrostatics]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Electrostatic Field Model

**Reference:** §1.2.2

---

## Model Equation

From Maxwell's equations (electrostatics): electric field $\mathbf{E} = -\operatorname{grad}\phi$, Gauss' law $\operatorname{div}(\epsilon\,\mathbf{E}) = \rho$:

$$-\operatorname{div}(\epsilon\,\operatorname{grad}\,\phi) = \rho \quad \text{in } \Omega$$

- $\phi$: electrostatic potential
- $\epsilon(\mathbf{x})$: permittivity (material parameter, may vary in space)
- $\rho$: charge density

For constant $\epsilon$: reduces to **Poisson equation** $-\Delta\phi = \rho/\epsilon$.

## Energy Functional

$$J(\phi) = \frac{1}{2}\int_\Omega \epsilon\,|\nabla\phi|^2\,\mathrm{d}\mathbf{x} - \int_\Omega \rho\,\phi\,\mathrm{d}\mathbf{x}$$

Same structure as [[Elastic-Membrane-Model]] but with spatially varying coefficient $\epsilon(\mathbf{x})$.

> [!info] Relation to diffusion
> The same PDE $-\operatorname{div}(\kappa\,\operatorname{grad}\,u) = f$ arises in heat conduction (§1.6) with $\kappa$ = thermal conductivity. The mathematical structure is identical — only the physical interpretation differs.

---

**Problems:** 1-7 | **Related:** [[Quadratic-Minimization-Problem]], [[Boundary-Conditions-Elliptic]]
