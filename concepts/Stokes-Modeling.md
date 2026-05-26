---
tags: [chapter-12, Stokes, fluid-flow, modeling]
first_appears: "[[Week-09-Stokes-I]]"
---

# Stokes Modeling

**Reference:** §12.1

---

## Physical setting

**Viscous incompressible fluid flow** at low Reynolds number. Navier-Stokes equations simplify to the **Stokes equations** when inertial terms are negligible:

$$\mathrm{Re} = \frac{\rho\,U\,L}{\mu} \ll 1$$

| Quantity | Role |
|----------|------|
| $\mathbf{u}$ | Velocity field |
| $p$ | Pressure (Lagrange multiplier for incompressibility) |
| $\mu$ | Dynamic viscosity |
| $\mathbf{f}$ | Body force |

## Stokes PDE system (§12.2.3)

$$-\mu\,\Delta \mathbf{u} + \nabla p = \mathbf{f} \quad \text{in } \Omega, \qquad \mathrm{div}\,\mathbf{u} = 0 \quad \text{in } \Omega$$

with no-slip BCs $\mathbf{u} = \mathbf{0}$ on $\partial\Omega$ (typical).

> [!info] Connection to Week 8
> [[Convection-Diffusion-Modeling]] assumed $\mathrm{div}\,\mathbf{v} = 0$ for the velocity field. Stokes determines both $\mathbf{u}$ and $p$ for viscous flow.

---

**Problems:** [[Stokes-Problems]] | **Related:** [[Stokes-Constrained-Variational]], [[Stokes-Saddle-Point]]
