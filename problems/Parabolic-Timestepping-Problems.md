---
tags: [problems, chapter-9, parabolic, timestepping, method-of-lines]
---

# Parabolic Timestepping Problems

Problems from Chapter 9 covering §9.2 topics: heat equation, spatial variational formulation, method of lines, implicit timestepping, convergence.

---

## Problem 9-1: Radau RK for Parabolic IBVPs

**Code folder:** `RadauThreeTimestepping` | **Sections:** §9.2.1, §9.2.2, §9.2.4, §9.2.7

**Concepts:** [[Heat-Equation]], [[Spatial-Variational-Formulation-Parabolic]], [[Method-of-Lines]], [[Timestepping-MOL]]

**Setup:** Heat equation on $]−1,1[^2$ with homogeneous Dirichlet BCs, moving laser beam source. Linear FEM, 2-stage Radau-3 RK timestepping.

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | 10 min | Derive spatial variational formulation |
| (b) | 20 min | Derive discrete evolution operator for Radau-3 applied to $\dot{y} = -y$ |
| (c) | 20 min | Implement `twoStageRadauTimeSteppingLinScalODE` in Eigen |
| (d) | 15 min | Convergence test for the scalar ODE — observe order 3 |
| (e) | 20 min | Write the Kronecker product linear system for 2-stage RK on MOL ODE |
| (f)–(g) | 15 min | Simplify the system exploiting the specific Radau Butcher tableau |
| (h)–(i) | 65 min | Implement `discreteEvolutionOperator` in LehrFEM++ (assembly + solve) |
| (j)–(k) | 35 min | Convergence study: spatial + temporal error |
| (l)–(m) | 40 min | Implement full solver, test on moving laser problem |

> [!tip] Key insight
> The Kronecker system $(\mathbf{I}_s \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A})$ for a 2-stage method is $2N \times 2N$. For general implicit RK you solve the full coupled system. For SDIRK methods (see 9-2) it decouples.

**LehrFEM++ patterns:** `AssembleMatrixLocally`, `AssembleVectorLocally`, `ReactionDiffusionElementMatrixProvider`, `ScalarLoadElementVectorProvider`

> [!abstract] Solution gist
> **(a)** Standard: multiply PDE by $v \in H^1_0$, integrate by parts → $m(\dot{u},v) + a(u,v) = \int_\Omega f\,v$. **(b)** Apply Radau-3 Butcher tableau to $\dot{y}=-y$: solve $2\times 2$ system for increments $\kappa_1, \kappa_2$, get stability function $R(z) = (1+z/3)/(1-2z/3+z^2/6)$. **(c–d)** Implement the scalar ODE stepper; observe order 3 convergence. **(e)** Kronecker form: $(\mathbf{I}_2 \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A})\vec{\kappa} = \text{rhs}$ — a $2N \times 2N$ system. **(f–g)** Use `Eigen::kroneckerProduct` for the system matrix; for Radau-3 $\mathcal{A}$ is full (not SDIRK), so no decoupling. **(h–i)** homework helper `dropMatrixRowsColumns` (problem-local utility, not LehrFEM++) zeros rows/columns for Dirichlet DOFs and sets diagonal to 1; LehrFEM++ uses `FixFlaggedSolutionComponents` on `COOMatrix`. Pre-factorize in constructor since $\tau$ is constant. **(j–k)** `discreteEvolutionOperator`: assemble time-dependent RHS via custom `TrapRuleLinFEElemVecProvider`, solve Kronecker system, update $\boldsymbol{\mu}^{(k+1)} = \boldsymbol{\mu}^{(k)} + \tfrac{3}{4}\kappa_1 + \tfrac{1}{4}\kappa_2$. **(l–m)** VTK output via `lf::io::VtkWriter`. Uniform $\tau$ → factorize once.

---

## Problem 9-2: Implicit Timestepping (SDIRK) for Parabolic IBVP

**Code folder:** `SDIRKMethodOfLines` | **Sections:** §9.2.2, §9.2.4, §9.2.7

**Concepts:** [[Spatial-Variational-Formulation-Parabolic]], [[Method-of-Lines]], [[Timestepping-MOL]], [[Essential-vs-Natural-BCs]]

**Setup:** Heat equation on 2D domain with **convective cooling** (Robin BC: $-\nabla u \cdot \mathbf{n} = cu$). SDIRK-2 timestepping.

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | 10 min | Spatial variational formulation — Robin BC creates boundary integral in $a(\cdot,\cdot)$ |
| (b)–(d) | 15 min | Element mass and stiffness matrices for unit triangle |
| (e)–(f) | 30 min | Boundary edge mass matrix $\int_e b_i b_j\,\mathrm{d}S$ via `MassEdgeMatrixProvider` |
| (g) | 15 min | SDIRK-2 stability function: prove $L(\pi)$-stability |
| (h) | 20 min | Determine order of SDIRK-2 from Butcher tableau |
| (i) | 30 min | Write Kronecker system for SDIRK-2 — exploit diagonal structure |
| (j)–(k) | 45 min | Implement SDIRK-2 timestepping in LehrFEM++ |
| (l)–(o) | 70 min | Convergence study, visualize temperature evolution |

> [!warning] Common mistake
> Robin BC: the boundary integral $c\int_{\partial\Omega} u\,v\,\mathrm{d}S$ goes into the **stiffness** bilinear form $a(\cdot,\cdot)$, not the mass form. This adds an edge mass matrix to $\mathbf{A}$.

**LehrFEM++ patterns:** `lf::uscalfe::MassEdgeMatrixProvider` (also valid as `lf::fe::MassEdgeMatrixProvider`; NPDERepo mostly uses `uscalfe`) or custom edge provider, `AssembleMatrixLocally`, `lf::mesh::utils::flagEntitiesOnBoundary`

> [!abstract] Solution gist
> **(a)** Robin BC: $-\nabla u \cdot \mathbf{n} = cu$ on $\partial\Omega$ → integration by parts gives $a(u,v) = \int_\Omega \nabla u \cdot \nabla v + c\int_{\partial\Omega} uv\,\mathrm{d}S$, $m(\dot{u},v) = \int_\Omega \dot{u}v$. **(b–d)** Element mass matrix on reference triangle: $\tfrac{|K|}{12}\begin{pmatrix}2&1&1\\1&2&1\\1&1&2\end{pmatrix}$. Stiffness: standard Laplacian + edge mass $\tfrac{c|e|}{6}\begin{pmatrix}2&1\\1&2\end{pmatrix}$ for boundary edges. **(e–f)** `lf::uscalfe::MassEdgeMatrixProvider` / `lf::fe::MassEdgeMatrixProvider` (or a custom provider like `LinearMassEdgeMatrixProvider` in `SDIRKMethodOfLines`) supplies the boundary 2×2 edge contributions scaled by $c$ and edge length. Assemble via `AssembleMatrixLocally(1, ...)` (codim 1). **(g)** Stability function $R(z) = \frac{1 - (1-\zeta)z}{(1-\zeta z)^2}$; $|R(z)| \to 0$ as $z \to -\infty$ → $L(\pi)$-stable. **(h)** Apply to $\dot{y}=-y$: observe order 2. **(i)** SDIRK: $\mathcal{A}$ lower-triangular → Kronecker system decouples into two $N \times N$ solves with same matrix $\mathbf{M} + \zeta\tau\mathbf{A}$. **(j–l)** Pre-factorize $\mathbf{M} + \zeta\tau\mathbf{A}$; each step: solve stage 1, then stage 2, then update $\boldsymbol{\mu}^{(k+1)} = \boldsymbol{\mu}^{(k)} + \tau\!\left((1-\zeta)\kappa_1 + \zeta\kappa_2\right)$ as in `SDIRKMethodOfLines`. Track thermal energy $E(t) = \sum_j \mu_j \int_\Omega b_j$. **(m–o)** VTK output; energy should decay monotonically.

---

## Problem 9-3: Decaying MOL Solution with Implicit Euler

**Code folder:** `—` | **Sections:** §9.2.3, §9.2.7

**Concepts:** [[Stability-Parabolic-Evolution]], [[Timestepping-MOL]], [[Method-of-Lines]]

> [!warning] Exam alert
> Discrete stability proof pattern relevant to **2022 Endterm 0-3** (degenerate parabolic). See [[Endterm-Ch9-Exam-Compendium#2022 Endterm 0-3]].

**Setup:** Purely theoretical. Prove that implicit Euler preserves the exponential decay from Lemma 9.2.3.8 at the discrete level.

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | 10 min | Show $\tilde{a}(v,v) := a(v,v) - \gamma\,m(v,v) \geq 0$ from Poincare-Friedrichs |
| (b) | 15 min | Implicit Euler for MOL with modified bilinear form $\tilde{a}$ |
| (c)–(d) | — | Diagonalization of the discrete system |
| (e) | 10 min | Bound $\|(\mathbf{I} + \tau\mathbf{M}^{-1}\mathbf{A})^{-1}\|$ for stability analysis |
| (f)–(h) | 20 min | Prove discrete energy norm is non-increasing: $\|\boldsymbol{\mu}^{(j)}\|_{\mathbf{M}} \leq \|\boldsymbol{\mu}^{(j-1)}\|_{\mathbf{M}}$ |

> [!tip] Key insight
> Implicit Euler inherits the continuous energy decay — the discrete analogue of Lemma 9.2.3.8 holds without any timestep restriction.

> [!abstract] Solution gist
> **(a)** Implicit Euler: $(\mathbf{M} + \tau\mathbf{A})\boldsymbol{\mu}^{(j)} = \mathbf{M}\boldsymbol{\mu}^{(j-1)}$. **(b)** Review diagonalization technique from §9.2.7.15. **(c)** Diagonalize via $\mathbf{A}\mathbf{T} = \mathbf{M}\mathbf{T}\mathbf{D}$, $\mathbf{T}^\top\mathbf{M}\mathbf{T} = \mathbf{I}$. Transform $\boldsymbol{\eta}^{(j)} = \mathbf{T}^\top\mathbf{M}\boldsymbol{\mu}^{(j)}$: implicit Euler becomes $\eta_i^{(j)} = \frac{1}{1+\tau\lambda_i}\eta_i^{(j-1)}$. **(d)** $\|\boldsymbol{\mu}\|_\mathbf{M}^2 = \|\boldsymbol{\eta}\|_2^2$, $\|\boldsymbol{\mu}\|_\mathbf{A}^2 = \sum \lambda_i |\eta_i|^2$. **(e)** From **(9.2.3.6)** ([[Stability-Parabolic-Evolution]]): $\lambda_i \geq \gamma > 0$. **(f)** Each component: $|\eta_i^{(j)}| = \frac{1}{1+\tau\lambda_i}|\eta_i^{(j-1)}| \leq \frac{1}{1+\gamma\tau}|\eta_i^{(j-1)}|$ → $\|\boldsymbol{\mu}^{(j)}\|_\mathbf{M} \leq \frac{1}{1+\gamma\tau}\|\boldsymbol{\mu}^{(j-1)}\|_\mathbf{M}$. **(g)** Same argument with $\lambda_i$ weights for $\|\cdot\|_\mathbf{A}$. **(h)** Discrete: $(1+\gamma\tau)^{-j} \leq e^{-\gamma j\tau}$ — consistent with continuous decay.

---

## Problem 9-17: Scalar Parabolic Evolution — Continuous & Discrete

**Code folder:** `ParabolicEvolutionAspects` (exam/HW PDF name; **not** in NPDERepo — theory aligns with exam; do not confuse with **9-12** `SobolevEvolutionProblem`) | **Sections:** §9.2.2, §9.2.4, §9.2.7

**Concepts:** [[Spatial-Variational-Formulation-Parabolic]], [[Method-of-Lines]], [[Timestepping-MOL]]

> [!warning] Exam alert
> This problem appeared as **2024 Endterm Problem 0-1**.

**Setup:** Parabolic evolution with $\int_{\partial\Omega} \dot{u}\,v\,\mathrm{d}S$ (boundary mass term) + Laplacian. Quadratic FEM.

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | — | Derive strong PDE form from variational formulation |
| (b) | — | Identify boundary conditions (natural Neumann) |
| (c) | 30 min | MOL ODE: identify $\mathbf{M}$ (includes boundary mass), $\mathbf{A}$ |
| (d) | — | Implicit Euler update formula |

> [!abstract] Solution gist
> **(a)** Unusual: $m(\dot{u},v) = \int_{\partial\Omega} \dot{u}\,v\,\mathrm{d}S$ (boundary mass, not volume). Strong form: $-\Delta u = 0$ in $\Omega$, $\dot{u} + \nabla u \cdot \mathbf{n} = 0$ on $\partial\Omega$ — the PDE is Laplace in the interior, evolution happens on the boundary only. **(b)** Natural Neumann BCs (no Dirichlet). **(c)** $\mathbf{M}_{ij} = \int_{\partial\Omega} b_i^h b_j^h\,\mathrm{d}S$ — **boundary** mass matrix assembled via `AssembleMatrixLocally(1, ...)`. $\mathbf{A}_{ij} = \int_\Omega \nabla b_i^h \cdot \nabla b_j^h$ — standard stiffness. Both use $S_2^0(\mathcal{M})$ (quadratic FEM). $\mathbf{M}$ is only s.p.s.d. (not s.p.d.) since interior DOFs don't appear. **(d)** Implicit Euler: $(\mathbf{M} + \tau\mathbf{A})\boldsymbol{\mu}^{(k+1)} = \mathbf{M}\boldsymbol{\mu}^{(k)}$. Questions: (A) $\mathbf{M}$ not s.p.d. → NO. (B) $\mathbf{A}$ not s.p.d. (constants in kernel with pure Neumann) → NO. (C–E) Depend on whether $u_0$ has a non-zero mean.

---

## Problem 9-20: MOL with SDIRK Timestepping

**Code folder:** `SDIRK` | **Sections:** §9.2.2, §9.2.4, §9.2.7, §9.2.8

> Exam PDFs name the folder `MOLSDIRK`; NPDERepo uses `SDIRK`.

**Concepts:** [[Method-of-Lines]], [[Timestepping-MOL]], [[Fully-Discrete-MOL-Convergence]]

> [!warning] Exam alert
> This problem appeared as **2025 Endterm Problem 0-2**.

**Setup:** Parabolic evolution with spatially varying coefficient $\sigma(\mathbf{x})$, Neumann BCs, quadratic FEM ($S_2^0(\mathcal{M})$).

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | 15 min | Derive strong PDE form + identify boundary conditions |
| (b) | — | Write MOL ODE with correct $\mathbf{M}$, $\mathbf{A}$ for $S_2^0$ |
| (c) | 20 min | Write SDIRK-2 update: two stages, same system matrix |
| (d) | — | Convergence analysis: balanced $h$-$\tau$ refinement |

> [!abstract] Solution gist
> **(a)** Strong form: $\sigma(\mathbf{x})\dot{u} - \Delta u = 0$ in $\Omega$, $\nabla u \cdot \mathbf{n} = 0$ on $\partial\Omega$ (Neumann). **(b)** $\mathbf{M}_{ij} = \int_\Omega \sigma b_i^h b_j^h$ (weighted mass), $\mathbf{A}_{ij} = \int_\Omega \nabla b_i^h \cdot \nabla b_j^h$ (stiffness). Use `ReactionDiffusionElementMatrixProvider(fe_space, mf_one, mf_zero)` for $\mathbf{A}$ and `(fe_space, mf_zero, mf_sigma)` for $\mathbf{M}$. **(c)** SDIRK-2: same as 9-2 structure. Two stages with matrix $\mathbf{M} + \zeta\tau\mathbf{A}$. Explicit block form: stage 1 RHS $= \mathbf{M}\boldsymbol{\mu}^{(k-1)}$, stage 2 RHS involves $\boldsymbol{\gamma}_1$ from stage 1. **(d)** Meta-Thm 9.2.8.5: $O(h^2 + \tau^2)$ in $H^1$ for $p=2$ quadratic FEM + order-2 SDIRK. Balance: $\tau \sim h$, so halving $h$ requires halving $\tau$. Reduction factor 100 → $h^2 = 10^{-2}$ → 10× refinement → $\lceil\log_2(10)\rceil = 4$ uniform refinements, $\tau$ reduced by factor 10.

---

## Problem 9-14: Two-Step Radau RK-SSM for the Heat Equation

**Code folder:** `—` (theory only) | **Sections:** §9.2.4, §9.2.7.1

**Concepts:** [[Method-of-Lines]], [[Heat-Equation]]

> [!warning] Exam alert
> This problem appeared as **2023 Endterm Problem 0-3**. See [[Endterm-Ch9-Exam-Compendium#2023 Endterm 0-3]].

**Setup:** Parabolic evolution with spatially varying density $\rho(\mathbf{x})$, Neumann BCs. Galerkin semi-discretization + 2-stage Radau-3 RK-SSM.

| Sub-task | Time | What it asks |
|----------|------|-------------|
| (a) | 20 min | Write MOL ODE matrices: $\mathbf{M}_{ij} = \int_\Omega \rho\,b_i b_j$, $\mathbf{A}_{ij} = \int_\Omega \nabla b_i \cdot \nabla b_j$, $\boldsymbol{\varphi} = \mathbf{0}$ |
| (b) | 30 min | Fill in the $2N \times 2N$ Kronecker system for the Radau-3 Butcher tableau applied to the MOL ODE |

> [!abstract] Solution gist
> **(a)** Weighted mass matrix from $\rho(\mathbf{x})$: use `ReactionDiffusionElementMatrixProvider(fe_space, mf_zero, mf_rho)`. Neumann BCs → no boundary modifications, $\boldsymbol{\varphi} = \mathbf{0}$. **(b)** Radau-3 Butcher matrix $\mathcal{A} = \begin{pmatrix}\frac{5}{12} & -\frac{1}{12}\\\frac{3}{4} & \frac{1}{4}\end{pmatrix}$. Kronecker system: $(\mathbf{I}_2 \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A})\begin{pmatrix}\boldsymbol{\kappa}_1\\\boldsymbol{\kappa}_2\end{pmatrix} = \begin{pmatrix}-\mathbf{A}\boldsymbol{\mu}^{(k)} + \boldsymbol{\varphi}(t_k + \frac{\tau}{3})\\-\mathbf{A}\boldsymbol{\mu}^{(k)} + \boldsymbol{\varphi}(t_k + \tau)\end{pmatrix}$. Update: $\boldsymbol{\mu}^{(k+1)} = \boldsymbol{\mu}^{(k)} + \frac{3}{4}\boldsymbol{\kappa}_1 + \frac{1}{4}\boldsymbol{\kappa}_2$. Non-SDIRK → must solve the full coupled $2N \times 2N$ system.

---

## Problem 9-11: Gauss-Lobatto IIIC Timestepping

**Code folder:** `GaussLobattoParabolic` | **Sections:** §9.2.7

**Concepts:** [[Timestepping-MOL]], [[Method-of-Lines]]

**Setup:** Alternative 2-stage implicit RK. Focus on implementing the coupled Kronecker system and convergence testing.

Sub-tasks: (a)–(i) covering Butcher tableau analysis, stability, implementation, convergence.

> [!abstract] Solution gist
> **(a)** Strong form: $\dot{u} - \Delta u = 0$ in $\Omega$, $u = g(t)$ on $\partial\Omega$ (Dirichlet). **(b)** MOL with interior/boundary DOF partitioning: $\begin{pmatrix}\mathbf{M}_{00} & \mathbf{M}_{0\partial}\\\mathbf{O} & \mathbf{O}\end{pmatrix}\dot{\boldsymbol{\mu}} + \begin{pmatrix}\mathbf{A}_{00} & \mathbf{A}_{0\partial}\\\mathbf{O} & \mathbf{I}\end{pmatrix}\boldsymbol{\mu} = \begin{pmatrix}\mathbf{0}\\g(t)\boldsymbol{\beta}_\partial\end{pmatrix}$. The boundary rows enforce $\mu_\partial = g(t)\boldsymbol{\beta}_\partial$. **(c–d)** Assemble extended $\tilde{\mathbf{M}}$, $\tilde{\mathbf{A}}$: identity block for boundary DOFs, zero mass rows for boundary. **(e)** $\tilde{\mathbf{M}} + \xi\tilde{\mathbf{A}}$ invertible for $\xi > 0$: interior block $\mathbf{M}_{00} + \xi\mathbf{A}_{00}$ is s.p.d., boundary block is $\xi\mathbf{I}$. **(f)** `RHSProvider`: precompute $\boldsymbol{\beta}_\partial$ (boundary node indicators) in constructor; `operator()(t)` returns $g(t)\boldsymbol{\beta}_\partial$ cheaply. **(g)** GL-IIIC Butcher matrix $\mathcal{A} = \begin{pmatrix}\frac{1}{2} & -\frac{1}{2}\\\frac{1}{2} & \frac{1}{2}\end{pmatrix}$ → $2N \times 2N$ Kronecker system. **(h)** Pre-factorize Kronecker matrix; per step: assemble RHS from $\tilde{\boldsymbol{\varphi}}$ at two stage times, solve, update. **(i)** GL-IIIC is order 2 with $p=1$ FEM → balance $\tau \sim h$ (since $H^1$ spatial error is $O(h)$, temporal is $O(\tau^2)$, balance at $\tau \sim h^{1/2}$, or if using $L^2$ norm: $\tau \sim h$).

---

## Problem 9-22: Heat Conduction in a Black Body

**Code folder:** `BlackBodyRadiation` | **Sections:** §9.2

> NPDERepo path: `developers/BlackBodyRadiation/mysolution/`

**Concepts:** [[Heat-Equation]], [[Boundary-Conditions-Elliptic]]

**Setup:** Non-linear radiation BC ($\mathbf{j} \cdot \mathbf{n} \propto u^4$). Requires Newton linearization at each timestep.

Sub-tasks: (a)–(f) covering variational formulation with non-linear BC, linearization, LehrFEM++ implementation.

> [!abstract] Solution gist
> **(a)** Minimization functional: $J(w) = \frac{1}{2}\int_\Omega |\nabla w|^2 + \frac{\sigma}{5}\int_{\partial\Omega} w^5 \,\mathrm{d}S - \int_\Omega w$. Setting $\langle DJ(u), v\rangle = 0$ recovers (9.22.1). **(b)** Strong form: $-\Delta u = 1$ in $\Omega$, $\nabla u \cdot \mathbf{n} + \sigma u^4 = 0$ on $\partial\Omega$ (Stefan-Boltzmann radiation BC). **(c)** $\boldsymbol{\rho}(\boldsymbol{\mu})_i = \int_{\partial\Omega} \left(\sum_j \mu_j b_j^h\right)^4 b_i^h \,\mathrm{d}S$ — nonlinear boundary integral. **(d)** `StefanBoltzmannElementVectorProvider::Eval`: for a boundary edge with nodes $p_1, p_2$, evaluate $u_h^4 b_i$ exactly. Since $u_h$ is piecewise linear on edges, $u_h^4$ is degree 4 → need appropriate quadrature (Simpson or exact for polynomials up to degree 5). **(e)** Newton: linearize $\sigma u^4$ → Jacobian adds $4\sigma \int_{\partial\Omega} u_h^3 w_h v_h \,\mathrm{d}S$ (edge mass matrix weighted by $4\sigma u_h^3$). Newton correction solves $\mathbf{A}\mathbf{w} + 4\sigma \mathbf{J}(\boldsymbol{\mu}^{(k)})\mathbf{w} = -\text{residual}$. **(f)** Fails when $u_h^{(k)} = 0$ everywhere: $4\sigma u_h^3 = 0$ → Jacobian reduces to pure Neumann Laplacian (singular).

---

## Problem 9-21: Magnetic Diffusion in a Wire

**Code folder:** `MagDiffWire` | **Sections:** §9.2

> NPDERepo path: `developers/MagDiffWire/mysolution/`

**Concepts:** [[Heat-Equation]], [[Method-of-Lines]], [[Assembly-Algorithm]]

**Setup:** Cylindrical geometry (1D radial), spatially varying coefficients. Method of lines + implicit timestepping.

Sub-tasks: (a)–(e).

> [!abstract] Solution gist
> **(a)** Strong form: $\sigma(\mathbf{x})\dot{u} - \text{div}\left(\frac{1}{\mu(\mathbf{x})}\nabla u\right) + U(t)\sigma(\mathbf{x}) = 0$ in $\Omega$, $u = 0$ on $\partial\Omega$, with constraint $\int_\Omega \sigma u = I(t)$. The extra scalar unknown $U(t)$ (voltage) couples to the current constraint. **(b)** MOL gives an $(N+1) \times (N+1)$ DAE-like system: $\mathbf{M}_{ij} = \int_\Omega \sigma b_i b_j$, $\mathbf{A}_{ij} = \int_\Omega \frac{1}{\mu}\nabla b_i \cdot \nabla b_j$, $d_i = \int_\Omega \sigma b_i$ (coupling vector), $q_i = d_i$, $\alpha = 0$, $\beta = 0$, $\boldsymbol{\varphi} = \mathbf{0}$, $\psi(t) = I(t)$. Note $\sigma = 0$ outside $\Omega_C$ → $\mathbf{M}$ is only s.p.s.d. **(c)** `buildExtMOLMatrices`: assemble $N \times N$ blocks via `ReactionDiffusionElementMatrixProvider`; then append row/column $N+1$ for the coupling terms $\mathbf{d}$, $\mathbf{q}$, $\alpha$, $\beta$ using `AddToEntry`. **(d)** SDIRK-2 on the extended system: same structure as 9-2 but with $(N+1) \times (N+1)$ matrices. **(e)** Implement `sdirkMagDiffWire`: pre-factorize $\tilde{\mathbf{M}} + \zeta\tau\tilde{\mathbf{A}}$, two-stage loop, record states via `rec` callback.

---

## Problem 9-23: Heat Equation on the CSE Mug

**Code folder:** `CSEMug` | **Sections:** §9.2

**Concepts:** [[Heat-Equation]], [[Method-of-Lines]], [[LehrFEM-Assembly-Patterns]]

Full pipeline problem: realistic geometry, assembly, timestepping, visualization. Single sub-task (a).

> [!abstract] Solution gist
> Fun problem — brew a drink. The actual coding exercise (if extended) would combine: Gmsh mesh of a mug cross-section, mixed-dimensional coupling (2D body + 1D handle), Robin BCs for convective cooling, implicit timestepping. Full LehrFEM++ pipeline: mesh loading → assembly → MOL ODE → SDIRK → VTK visualization.

---

**Related concepts:** [[Heat-Equation]], [[Spatial-Variational-Formulation-Parabolic]], [[Method-of-Lines]], [[Timestepping-MOL]], [[Stiffness-Parabolic]], [[Fully-Discrete-MOL-Convergence]], [[Formulas-Timestepping]], [[LehrFEM-Solver-Convergence-Patterns]]

**Endterm prep:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Ch9-Exam-Compendium]] | [[Endterm-Ch9-Homework-Walkthrough]]
