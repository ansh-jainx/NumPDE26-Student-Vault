---
tags: [chapter-12, Stokes, constrained, variational]
first_appears: "[[Week-09-Stokes-I]]"
---

# Stokes Constrained Variational Formulation

**Reference:** §12.2.1

---

## Formulation

Minimize viscous energy subject to $\mathrm{div}\,\mathbf{u} = 0$:

$$\mathbf{u} \in H_0^1(\mathrm{div}\,0, \Omega) := \{\mathbf{v} \in (H_0^1(\Omega))^d : \mathrm{div}\,\mathbf{v} = 0\}$$

$$\int_\Omega \mu\,D\mathbf{u} : D\mathbf{w}\,\mathrm{d}\mathbf{x} = \int_\Omega \mathbf{f} \cdot \mathbf{w}\,\mathrm{d}\mathbf{x} \quad \forall \mathbf{w} \in H_0^1(\mathrm{div}\,0, \Omega)$$

where $D\mathbf{u} = \frac{1}{2}(\nabla \mathbf{u} + \nabla \mathbf{u}^T)$ is the strain rate tensor.

## Relation to saddle-point form

The divergence constraint $\mathrm{div}\,\mathbf{u} = 0$ is handled implicitly by restricting to the constrained space. The [[Stokes-Saddle-Point]] formulation introduces pressure $p$ as a Lagrange multiplier and is more practical for FEM.

---

**Problems:** 12-4 | **Related:** [[Stokes-Saddle-Point]], [[Stokes-Modeling]], [[Linear-Variational-Problem]]
