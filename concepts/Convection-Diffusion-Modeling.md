---
tags: [chapter-10, convection-diffusion, modeling, fluid-flow]
first_appears: "[[Week-08-Convection-Diffusion]]"
---

# Convection-Diffusion Modeling

**Reference:** §10.1.1–§10.1.4

---

## Stationary BVP (§10.2.0.1)

Incompressible flow ($\mathrm{div}\,\mathbf{v} = 0$), diffusion + advection:

$$-\varepsilon\,\Delta u + \mathbf{v}(\mathbf{x}) \cdot \nabla u = f \quad \text{in } \Omega, \qquad u = 0 \text{ on } \partial\Omega$$

- $\varepsilon > 0$: diffusion coefficient (after scaling, $\|\mathbf{v}\|_{L^\infty} = 1$)
- $\mathbf{v}$: velocity field (from fluid flow model §10.1.1)
- Physical origin: heat conduction in a moving fluid (§10.1.2) — extends [[Heat-Equation]] with advection term

> [!info] Variational form (§10.2.0.2)
> **Do not integrate by parts on the convection term!**
> Find $u \in H_0^1(\Omega)$:
> $$\varepsilon\int_\Omega \nabla u \cdot \nabla w\,\mathrm{d}\mathbf{x} + \int_\Omega (\mathbf{v} \cdot \nabla u)\,w\,\mathrm{d}\mathbf{x} = \int_\Omega f\,w\,\mathrm{d}\mathbf{x} \quad \forall w \in H_0^1(\Omega)$$

The convection bilinear form $c(u,w) = \int_\Omega (\mathbf{v}\cdot\nabla u)\,w$ is **non-symmetric** — standard coercivity arguments from Ch 1 do not apply directly.

## Inflow / Outflow (§10.2.1.10–11)

For $\varepsilon \to 0$ (pure transport): Dirichlet data only on **inflow** boundary:

$$\Gamma_{\mathrm{in}} = \{\mathbf{x} \in \partial\Omega : \mathbf{v}(\mathbf{x}) \cdot \mathbf{n}(\mathbf{x}) < 0\}, \qquad \Gamma_{\mathrm{out}} = \{\mathbf{x} : \mathbf{v} \cdot \mathbf{n} > 0\}$$

## Transient case (§10.1.4, §10.3.1)

$$\frac{\partial u}{\partial t} - \varepsilon\,\Delta u + \mathbf{v} \cdot \nabla u = f \quad \text{in } \Omega \times\,]0,T[$$

Discretized via [[MOL-Convection-Diffusion]] (spatial FEM + [[Timestepping-MOL]]).

---

**Problems:** [[Convection-Diffusion-Problems]] | **Related:** [[Singular-Perturbation]], [[Heat-Equation]], [[Boundary-Conditions-Elliptic]]
