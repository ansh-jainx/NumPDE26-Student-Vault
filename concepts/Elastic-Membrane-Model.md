---
tags: [chapter-1, modeling, elliptic, membrane]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Elastic Membrane Model

**Reference:** §1.2

---

## Model Equations

**1D (elastic string):** displacement $u(x)$ of a string under load $f(x)$:

$$-u''(x) = f(x) \quad \text{in } ]a,b[, \qquad u(a) = u(b) = 0$$

**2D (elastic membrane):** displacement $u(\mathbf{x})$ of a membrane clamped at boundary:

$$-\Delta u = f \quad \text{in } \Omega, \qquad u = 0 \quad \text{on } \partial\Omega$$

## Dirichlet Principle

The solution $u$ minimizes the **total potential energy**:

$$J(u) = \underbrace{\frac{1}{2}\int_\Omega |\nabla u|^2\,\mathrm{d}\mathbf{x}}_{\text{elastic energy}} - \underbrace{\int_\Omega f\,u\,\mathrm{d}\mathbf{x}}_{\text{work of load}}$$

This is the prototypical [[Quadratic-Minimization-Problem]].

> [!tip] Why this matters
> Every second-order elliptic BVP can be cast as energy minimization → variational problem → FEM. The membrane is the simplest example of this pipeline.

---

**Problems:** 1-2, 1-4 | **Related:** [[Electrostatic-Field-Model]], [[Linear-Variational-Problem]]
