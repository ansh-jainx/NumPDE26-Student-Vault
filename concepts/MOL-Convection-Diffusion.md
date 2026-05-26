---
tags: [chapter-10, parabolic, method-of-lines, convection]
first_appears: "[[Week-08-Convection-Diffusion]]"
---

# MOL for Convection-Diffusion

**Reference:** §10.3.1

---

## Transient IBVP

$$\frac{\partial u}{\partial t} - \varepsilon\,\Delta u + \mathbf{v} \cdot \nabla u = f \quad \text{in } \Omega \times\,]0,T[, \qquad u(\cdot,0) = u_0$$

Same spatial variational structure as stationary case, with mass term $m(\dot{u}, v) = \int_\Omega \dot{u}\,v\,\mathrm{d}\mathbf{x}$.

## Method of lines

Galerkin in space $\Rightarrow$ [[Method-of-Lines]] ODE:

$$\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}(t)$$

- $\mathbf{M}$: mass matrix
- $\mathbf{A}$: stiffness + **convection** (non-symmetric) — assembled via `ConvBLFMatrixProvider`
- Timestep with [[Timestepping-MOL]] from Week 7

> [!warning] Stiffness in time
> Advection imposes a **CFL-like** constraint on explicit methods: $\tau = O(h / \|\mathbf{v}\|)$ for stability. Use implicit or $L(\pi)$-stable RK (same lesson as [[Stiffness-Parabolic]]).

## Inflow BCs for transient problems

Dirichlet data on $\Gamma_{\mathrm{in}}$ only (§10.2.1.11); outflow is natural.

---

**Problems:** [[Convection-Diffusion-Problems]] | **Related:** [[Convection-Diffusion-Modeling]], [[Method-of-Lines]], [[Timestepping-MOL]], [[Week-07-Parabolic-IBVPs]]
