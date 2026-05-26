---
tags: [chapter-9, timestepping, Euler, Crank-Nicolson, Runge-Kutta, SDIRK, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Timestepping for Method-of-Lines ODE

**Reference:** §9.2.7

---

## Schemes Applied to $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$

| Scheme | Update | Order | $L(\pi)$? |
|--------|--------|-------|-----------|
| Explicit Euler | $\boldsymbol{\mu}^{(j)} = \boldsymbol{\mu}^{(j-1)} + \tau\mathbf{M}^{-1}(\boldsymbol{\varphi}_{j-1} - \mathbf{A}\boldsymbol{\mu}^{(j-1)})$ | 1 | No |
| Implicit Euler | $(\mathbf{M}+\tau\mathbf{A})\boldsymbol{\mu}^{(j)} = \mathbf{M}\boldsymbol{\mu}^{(j-1)} + \tau\boldsymbol{\varphi}_j$ | 1 | Yes |
| Crank-Nicolson | $(\mathbf{M}+\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j)} = (\mathbf{M}-\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j-1)} + \frac{\tau}{2}(\boldsymbol{\varphi}_j + \boldsymbol{\varphi}_{j-1})$ | 2 | No |
| SDIRK-2 | Two stages, each solving $(\mathbf{M}+\gamma\tau\mathbf{A})\mathbf{k}_i = \text{rhs}$ | 2 | Yes |

## General RK for MOL (§9.2.7.6)

$s$-stage RK yields a $Ns$-system in Kronecker form: $(\mathbf{I}_s \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A})\vec{\kappa} = \text{rhs}$.

For **SDIRK** methods: the Butcher matrix $\mathcal{A}$ is lower-triangular with constant diagonal → same system matrix for all stages, factorize once.

> [!tip] $L(\pi)$-stability
> $|S(z)| \to 0$ as $\text{Re}(z) \to -\infty$. This ensures large eigencomponents are damped, matching continuous physics. Crank-Nicolson maps $z = -\infty$ to $|S| = 1$ — causes oscillatory artifacts.

---

**Problems:** 9-1 (Radau), 9-2 (SDIRK-2), 9-11 (Gauss-Lobatto) | **Related:** [[Stiffness-Parabolic]], [[Fully-Discrete-MOL-Convergence]]
