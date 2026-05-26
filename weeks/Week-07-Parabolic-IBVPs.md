---
tags: [week-7, chapter-9, parabolic, heat-equation, method-of-lines, exam-critical]
---

# Week 7 — Parabolic Initial-Boundary Value Problems

**Sections:** §9.2.1–9.2.8 | **Chapter 9: Second-Order Linear Evolution Problems**

---

## Overview

This week moves from stationary elliptic BVPs to **time-dependent** problems. The [[Heat-Equation]] is the model parabolic PDE. Pipeline: [[Spatial-Variational-Formulation-Parabolic]] → [[Method-of-Lines]] → [[Timestepping-MOL]] → [[Fully-Discrete-MOL-Convergence]]. Central challenge: [[Stiffness-Parabolic]] — explicit integrators need $\tau = O(h^2)$; use $L(\pi)$-stable schemes. Code: [[LehrFEM-Solver-Convergence-Patterns]]; formulas: [[Formulas-Timestepping]].

```mermaid
graph LR
    A[Parabolic IBVP] -->|test + integrate by parts| B[Spatial Variational Form]
    B -->|Galerkin FEM| C["MOL ODE: Mμ̇ + Aμ = φ"]
    C -->|implicit RK| D[Fully Discrete Scheme]
    style D fill:#f96
```

---

## Theory Gist

### §9.2.1 — Heat Equation

> [!info] Core PDE
> $$\frac{\partial}{\partial t}(\rho u) - \operatorname{div}(\kappa\,\operatorname{grad}\, u) = f \quad \text{in } \Omega \times\, ]0,T[$$
> From: energy conservation + Fourier's law $\mathbf{j} = -\kappa\,\operatorname{grad}\,u$.
> Needs: initial condition $u(\mathbf{x},0) = u_0(\mathbf{x})$ + boundary conditions (Dirichlet/Neumann/radiation — same as stationary case).

> [!warning] Compatibility
> For Dirichlet BCs: $g(\mathbf{x},0) = u_0(\mathbf{x})$ on $\partial\Omega$.

Key insight: an evolution PDE is an ODE in an infinite-dimensional function space. This motivates [[Method-of-Lines]].

### §9.2.2 — Spatial Variational Formulation

See [[Spatial-Variational-Formulation-Parabolic]].

Test with $v \in H_0^1(\Omega)$ (spatial only, no $t$ dependence), integrate by parts in space:

$$m(\dot{u}(t), v) + a(u(t), v) = \ell(t)(v) \quad \forall v \in V_0, \qquad u(0) = u_0$$

| Bilinear form | Formula | Role |
|---|---|---|
| $m(u,v)$ | $\int_\Omega \rho\,u\,v\,\mathrm{d}\mathbf{x}$ | mass (s.p.d.) |
| $a(u,v)$ | $\int_\Omega \kappa\,\nabla u \cdot \nabla v\,\mathrm{d}\mathbf{x}$ | stiffness (s.p.d.) |
| $\ell(t)(v)$ | $\int_\Omega f(\cdot,t)\,v\,\mathrm{d}\mathbf{x}$ | load |

### §9.2.3 — Stability (Energy Decay)

See [[Stability-Parabolic-Evolution]].

> [!theorem] Lemma 9.2.3.8 — Exponential decay
> For $f \equiv 0$: $\|u(t)\|_m \leq e^{-\gamma t}\|u_0\|_m$ and $\|u(t)\|_a \leq e^{-\gamma t}\|u_0\|_a$, where $\gamma$ is the Poincare-Friedrichs constant.

Physical meaning: parabolic evolutions **dissipate energy**. High-frequency Fourier modes decay fastest.

### §9.2.4 — Method of Lines ODE

See [[Method-of-Lines]].

Galerkin in space with basis $\{b_i^h\}$, expand $u_h(t) = \sum \mu_i(t)\,b_i^h$:

$$\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}(t), \qquad \boldsymbol{\mu}(0) = \boldsymbol{\mu}_0$$

- $\mathbf{A}$: stiffness matrix, $(\mathbf{A})_{ij} = a(b_j^h, b_i^h)$
- $\mathbf{M}$: mass matrix, $(\mathbf{M})_{ij} = m(b_j^h, b_i^h)$
- $\boldsymbol{\varphi}(t)$: load vector, $(\boldsymbol{\varphi})_i = \ell(t)(b_i^h)$

### §9.2.7 — Timestepping

See [[Timestepping-MOL]].

| Scheme | Update rule | Order | Stability |
|--------|-----------|-------|-----------|
| Explicit Euler | $\mathbf{M}\boldsymbol{\mu}^{(j)} = (\mathbf{M} - \tau\mathbf{A})\boldsymbol{\mu}^{(j-1)} + \tau\boldsymbol{\varphi}(t_{j-1})$ | 1 | $\tau < 2/\lambda_{\max}$ |
| Implicit Euler | $(\mathbf{M}+\tau\mathbf{A})\boldsymbol{\mu}^{(j)} = \mathbf{M}\boldsymbol{\mu}^{(j-1)} + \tau\boldsymbol{\varphi}(t_j)$ | 1 | Unconditional |
| Crank-Nicolson | $(\mathbf{M}+\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j)} = (\mathbf{M}-\frac{\tau}{2}\mathbf{A})\boldsymbol{\mu}^{(j-1)} + \frac{\tau}{2}(\boldsymbol{\varphi}_j + \boldsymbol{\varphi}_{j-1})$ | 2 | A-stable, not $L(\pi)$ |

> [!warning] Stiffness — why explicit methods fail
> Diagonalization: $\mathbf{A}\boldsymbol{\psi}_i = \lambda_i\mathbf{M}\boldsymbol{\psi}_i$ gives $\lambda_{\max} = O(h^{-2})$.
> Explicit Euler needs $\tau < 2/\lambda_{\max} = O(h^2)$. Stability kills efficiency.
> **Use $L(\pi)$-stable implicit methods** (implicit Euler, SDIRK-2, Radau collocation).

### §9.2.8 — Convergence of Fully Discrete Scheme

See [[Fully-Discrete-MOL-Convergence]].

> [!theorem] Meta-Theorem 9.2.8.5
> Degree-$p$ FEM + order-$q$ $L(\pi)$-stable RK: total error $\leq C(h^p + \tau^q)$.

Balanced refinement: to halve the error, reduce $h$ by $2^{1/p}$ and $\tau$ by $2^{1/q}$ simultaneously.

---

## Method Recipes

### Recipe 1: Derive the spatial variational formulation for a given IBVP

1. Identify the PDE, boundary conditions, and initial conditions
2. Multiply PDE by test function $v$ from the **correct** test space (e.g., $H_0^1$ for homogeneous Dirichlet)
3. Integrate over $\Omega$
4. Integration by parts in space (Green's first formula) on the second-order spatial term
5. Apply boundary conditions to handle boundary terms
6. Identify $m(\cdot,\cdot)$, $a(\cdot,\cdot)$, $\ell(t)(\cdot)$

> [!tip] Common variant
> For Neumann/Robin BCs, the test space is $H^1(\Omega)$ (not $H_0^1$) and boundary integrals survive — they become part of $a(\cdot,\cdot)$ or $\ell(t)(\cdot)$. See Problems 9-2, 9-20.

### Recipe 2: Set up the MOL ODE in LehrFEM++

1. **Mesh**: load or generate a triangular mesh $\mathcal{M}$ of $\Omega$
2. **FE space**: create `lf::uscalfe::FeSpaceLagrangeO1` (linear) or `lf::uscalfe::FeSpaceLagrangeO2` (quadratic)
3. **Stiffness matrix $\mathbf{A}$**: assemble via `lf::uscalfe::ReactionDiffusionElementMatrixProvider` with diffusion coefficient $\kappa$
4. **Mass matrix $\mathbf{M}$**: `ReactionDiffusionElementMatrixProvider(fe_space, mf_zero, mf_rho)` — cell assembly (`codim = 0`)
5. **Boundary terms**: Robin/Neumann via `lf::uscalfe::MassEdgeMatrixProvider` (docs also provide `lf::fe::MassEdgeMatrixProvider`; NPDERepo mostly uses `uscalfe`) or custom edge provider as in `SDIRKMethodOfLines` — edge assembly (`codim = 1`; see Problem 9-2)
6. **Load vector $\boldsymbol{\varphi}(t)$**: assemble via `lf::uscalfe::ScalarLoadElementVectorProvider`, re-assemble or update at each time level if $f$ depends on $t$
7. **Essential BCs**: apply via flagging/elimination (cf. §2.7.6)

### Recipe 3: Implement implicit Euler timestepping

```
for j = 1, ..., M:
    solve (M + τ·A) μ^(j) = M·μ^(j-1) + τ·φ(t_j)
```

- Pre-factorize $(\mathbf{M} + \tau\mathbf{A})$ if $\tau$ is uniform (Eigen `SparseLU` or `SimplicialLDLT`)
- For non-uniform $\tau$: refactorize or use iterative solver

### Recipe 4: Implement SDIRK-2 timestepping (order 2, $L(\pi)$-stable)

Butcher tableau: $\gamma = 1 - \frac{1}{\sqrt{2}}$

$$\begin{array}{c|cc} \gamma & \gamma & 0 \\ 1 & 1-\gamma & \gamma \\ \hline & 1-\gamma & \gamma \end{array}$$

Each stage solves: $(\mathbf{M} + \gamma\tau\mathbf{A})\mathbf{k}_i = \text{rhs}_i$ — same matrix for both stages, factorize once.

### Recipe 5: Implement general $s$-stage RK for MOL ODE

Per §9.2.7.6: solve the $Ns \times Ns$ system (Kronecker product form):
$$(\mathbf{I}_s \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A})\begin{pmatrix}\boldsymbol{\kappa}_1 \\ \vdots \\ \boldsymbol{\kappa}_s\end{pmatrix} = \text{rhs}$$

For SDIRK methods this decouples into $s$ independent $N \times N$ solves with the **same** system matrix.

---

## Homework Problems

> [[Parabolic-Timestepping-Problems]]

| Problem | Title | Sub-tasks | Code folder | Key skills |
|---------|-------|-----------|-------------|------------|
| **9-1** | Radau RK for Parabolic IBVPs | a–m | `RadauThreeTimestepping` | Variational form, RK Butcher scheme, LehrFEM++ assembly, convergence testing |
| **9-2** | Implicit Timestepping (SDIRK) for Parabolic IBVP | a–o | `SDIRKMethodOfLines` | Robin BCs, SDIRK-2 implementation, edge mass matrix, $L(\pi)$-stability proof |
| **9-3** | Decaying MOL Solution with Implicit Euler | a–h | *(theory only)* | Diagonalization, discrete energy decay, purely theoretical |
| **9-11** | Gauss-Lobatto IIIC Timestepping | a–i | `GaussLobattoParabolic` | Alternative implicit RK, Kronecker product system |
| **9-14** | Two-Step Radau RK for Heat Equation | a–b | *(theory only)* | Butcher tableau analysis |
| **9-17** | Scalar Parabolic Evolution: Continuous & Discrete | a–d | `ParabolicEvolutionAspects` *(theory write-up; no NPDERepo folder — distinct from Problem 9-12)* | Boundary mass matrix, strong form derivation — **also appeared as 2024 Endterm 0-1** |
| **9-20** | MOL with SDIRK Timestepping | a–d | exam `MOLSDIRK` → repo `SDIRK` | Quadratic FEM ($S_2^0$), SDIRK stages — **also appeared as 2025 Endterm 0-2** |
| **9-21** | Magnetic Diffusion in a Wire | a–e | `MagDiffWire` | Cylindrical geometry, spatially varying coefficients |
| **9-22** | Heat Conduction in a Black Body | a–f | `BlackBodyRadiation` | Non-linear radiation BC, Newton linearization |
| **9-23** | Solving Heat Eq on CSE Mug | a | `CSEMug` | Full pipeline on realistic geometry |

---

## Exam Problems

> Full course bank: [[Exam-Master-Bank#Ch9]] | Full course: [[Exam-Prep-Index]] | Endterm prep: [[Endterm-Prep-Ch9-Ch12]]

| Year | Exam | Problem | Topic | HW / note |
|------|------|---------|-------|-----------|
| **2025** | Final (Winter) | 1-2 | Heat Conduction in a Black Body | 9-22 BlackBodyRadiation; [[Exam-Deep-Parabolic-MOL]] |
| **2025** | Final (Summer) | 1-1 | Magnetic Diffusion in a Wire | 9-21 MagDiffWire; [[Exam-Deep-Parabolic-MOL]] |
| **2025** | Endterm | 0-2 | Method-of-Lines with SDIRK timestepping | 9-20 MOLSDIRK; [[Exam-Deep-Parabolic-MOL]] |
| **2024** | Final (Winter) | 1-1 | Implicit Runge-Kutta Timestepping for a Degenerate… | — IRKDegenerateEvl; [[Exam-Deep-Parabolic-MOL]] |
| **2024** | Endterm | 0-1 | Scalar Parabolic Evolution Problems: Continuous an… | 9-17 ParabolicEvolutionAspects; [[Exam-Deep-Parabolic-MOL]] |
| **2023** | Final (Winter) | 1-1 | Finite-Element Discretization of the Guyer-Krumhan… | — GuyerKrumhansl; [[Exam-Deep-Parabolic-MOL]] |
| **2023** | Endterm | 0-3 | Two-Step Radau Runge-Kutta Single-Step Method for … | — [[Exam-Deep-Parabolic-MOL]] |
| **2022** | Final (Summer) | 1-2 | Leapfrog Timestepping for Dissipative Wave Equatio… | — [[Exam-Deep-Parabolic-MOL]] |
| **2022** | Endterm | 0-3 | A Degenerate Parabolic Evolution Problem | — [[Exam-Deep-Parabolic-MOL]] |
| **2022** | Endterm | 0-2 | Some Aspects of Runge-Kutta Single-Step Methods | — — |
| **2021** | Endterm | 0-3 | Parabolic Timestepping with a 2-stage Implicit Run… | — [[Exam-Deep-Parabolic-MOL]] |
| **2021** | Endterm | 0-2 | Stiffness of Initial-Value Problems | — — |
| **2021** | Endterm | 0-1 | Embedded Runge-Kutta Single-Step Methods | — — |
| **2020** | Final (Summer) | 0-3 | Gauss-Lobatto IIIC Timestepping | — [[Exam-Deep-Parabolic-MOL]] |

---

## Connections

| This week | Builds on | Feeds into |
|-----------|-----------|------------|
| Heat equation | Stationary diffusion (§1.6), [[Boundary-Conditions-Elliptic]] | [[Week-08-Convection-Diffusion]] |
| Spatial variational form | [[Linear-Variational-Problem]], [[Sobolev-Spaces]] | [[Week-09-Stokes-I]] |
| Method of lines | [[Galerkin-Discretization]], [[Assembly-Algorithm]] | [[Week-12-FEEC-II-and-EM-Waves]] |
| Stiffness / stability | Ch 7 (stiff IVPs), RK methods | CFL condition for waves (§9.3.5) |
| Spatial error $h^p$ in meta-theorem | [[A-Priori-FEM-Error-Estimates]] (Ch3), [[Cea-Lemma]] | Understanding balanced refinement |

---

## Exam Checklist

- [ ] Derive spatial variational formulation from a given parabolic IBVP with specific BCs
- [ ] Identify $m$, $a$, $\ell$ and the correct test/trial space for Dirichlet, Neumann, or Robin BCs
- [ ] Set up the MOL ODE: write down $\mathbf{M}$, $\mathbf{A}$, $\boldsymbol{\varphi}$ for a given problem
- [ ] Write the fully discrete scheme for implicit Euler, Crank-Nicolson, or a given RK Butcher tableau
- [ ] Explain $\tau = O(h^2)$ constraint for explicit methods via diagonalization argument
- [ ] State convergence meta-theorem: error $\leq C(h^p + \tau^q)$ and derive balanced refinement
- [ ] Explain $L(\pi)$-stability: what it means, why it matters, which methods have it
- [ ] Explain where the $h^p$ spatial convergence rate in the meta-theorem comes from ([[A-Priori-FEM-Error-Estimates|a priori FEM error estimates]], Ch3)
