**ETH Zurich 401-0674-00L | Spring Term 2026**

Setup: [[README]] — clone vault, Obsidian install, NPDERepo workflow.

---

## Weekly Handouts

| Week | Chapter | Topic |
|------|---------|-------|
| 1 | Ch 1 (I) | [[Week-01-Elliptic-BVPs-I]] — Elastic membranes, electrostatic fields, quadratic minimization, Sobolev spaces, linear variational problems |
| 2 | Ch 1 (II) | [[Week-02-Elliptic-BVPs-II]] — Equilibrium models & BVPs, diffusion models, boundary conditions, 2nd-order elliptic variational problems, essential vs natural BCs |
| 3 | Ch 2 (I) | [[Week-03-FEM-I]] — Galerkin discretization principles, linear FEM for 1D and 2D BVPs |
| 4 | Ch 2 (II) | [[Week-04-FEM-II]] — Building blocks of FEM, Lagrangian FEM, mesh data structures, assembly, local computations, essential BCs |
| 5 | Ch 2–3 | [[Week-05-Parametric-FEM-and-Error]] — Parametric FEM, abstract Galerkin error estimates, empirical convergence |
| 6 | Ch 3 | [[Week-06-Convergence-and-Accuracy]] — A priori error estimates, elliptic regularity, variational crimes, code validation |
| 7 | Ch 9 | [[Week-07-Parabolic-IBVPs]] — Heat equation, method of lines, timestepping, convergence of fully discrete schemes |
| 8 | Ch 10 | [[Week-08-Convection-Diffusion]] — Convection-diffusion: fluid flow, singular perturbation, upwinding, streamline diffusion |
| 9 | Ch 12 (I) | [[Week-09-Stokes-I]] — Stokes: modeling, constrained variational & saddle point formulations |
| 10 | Ch 12 (II) | [[Week-10-Stokes-II]] — Stokes FEM: pressure instability, Taylor-Hood, Crouzeix-Raviart |
| 11 | Ch 13 (I) | [[Week-11-FEEC-I]] — FEEC: differential forms, exterior calculus, Sobolev spaces of forms |
| 12 | Ch 13 (II) | [[Week-12-FEEC-II-and-EM-Waves]] — FEEC: cochain calculus, Whitney forms, EM wave equations |
| 13 | Ch 13 (III) | [[Week-13-FEEC-Magnetostatics]] — Magnetostatics: potentials, saddle-point, discrete LBB |

---

## Exam Prep (full course)

All midterms, endterms, and summer/winter finals (2018–2026). Tiered depth: master bank + theme deep dives.

| Document | Audience |
|----------|----------|
| [[Exam-Prep-Index]] | **Start here** — study paths, document map |
| [[Exam-Master-Bank]] | Searchable index of all ~75 exam problems |
| [[Midterm-Compendium]] | Midterms 2021–2026 (Ch.1–3) |
| [[Finals-Compendium]] | Summer/winter finals (coding-heavy) |
| [[Exam-Recurring-Patterns-Global]] | Frequency matrix across all exams |
| [[Exam-Folder-Crosswalk]] | Exam PDF folder ↔ HW ↔ NPDERepo |
| [[Exam-Problem-Types-Full-Course]] | Types A–G (full course) |

Theme deep dives: [[Exam-Deep-Elliptic-Weak-Form]], [[Exam-Deep-Convection-Upwind]], [[Exam-Deep-Parabolic-MOL]], [[Exam-Deep-Stokes-Mixed]], [[Exam-Deep-Convergence-Plots]], [[Exam-Deep-Element-Matrices]], [[Exam-Deep-FEEC-Maxwell]]

---

## Endterm Prep (Ch.9 & Ch.12)

**Exam scope:** Chapter 9 (parabolic / MOL / timestepping) + Chapter 12 (Stokes FEM). Out of scope: Ch.10, Ch.13, midterms.

| Document | Audience |
|----------|----------|
| [[Endterm-Prep-Ch9-Ch12]] | **Start here** — hub, checklist, document map |
| [[Endterm-Ch9-Student-Handout]] | Ch.9 condensed reference + practice |
| [[Endterm-Ch12-Student-Handout]] | Ch.12 condensed reference + practice |
| [[Endterm-Problem-Types-Recipes]] | Exam Types A–G recipes |
| [[Endterm-Ch9-Exam-Compendium]] | All Ch.9 endterm problems 2021–2025 |
| [[Endterm-Ch12-Exam-Compendium]] | 2025 Stokes endterm deep dive |
| [[Endterm-Ch9-Homework-Walkthrough]] | Priority Ch.9 homework for endterm |
| [[Endterm-Ch12-Homework-Walkthrough]] | Priority Ch.12 homework for endterm |
| [[Endterm-Practice-Set]] | Mock questions + self-check answers |
| [[Endterm-Code-Cheatsheet]] | MOL / SDIRK / Stokes code patterns |

Also: [[Endterm-Scope-and-Sources]], [[Endterm-Recurring-Patterns]]

---

## Concept Cards

### Chapter 1 — Elliptic BVPs
- [[Elastic-Membrane-Model]]
- [[Electrostatic-Field-Model]]
- [[Quadratic-Minimization-Problem]]
- [[Sobolev-Spaces]]
- [[Linear-Variational-Problem]]
- [[Lax-Milgram-Theorem]]
- [[Boundary-Conditions-Elliptic]]
- [[Essential-vs-Natural-BCs]]

### Chapter 2 — Finite Element Methods
- [[Galerkin-Discretization]]
- [[Galerkin-Matrix]]
- [[Linear-FEM-1D]]
- [[Triangular-Linear-FEM-2D]]
- [[Lagrangian-FEM]]
- [[Mesh-Data-Structures]]
- [[Assembly-Algorithm]]
- [[Local-Computations]]
- [[Essential-BC-Treatment]]
- [[Parametric-FEM]]

### Chapter 3 — FEM Convergence
- [[Galerkin-Orthogonality]]
- [[Cea-Lemma]]
- [[Algebraic-vs-Exponential-Convergence]]
- [[Interpolation-Error-Estimates]]
- [[A-Priori-FEM-Error-Estimates]]
- [[Elliptic-Regularity]]
- [[Variational-Crimes]]
- [[FEM-Code-Validation]]

### Chapter 9 — Parabolic IBVPs
- [[Heat-Equation]]
- [[Spatial-Variational-Formulation-Parabolic]]
- [[Stability-Parabolic-Evolution]]
- [[Method-of-Lines]]
- [[Stiffness-Parabolic]]
- [[Timestepping-MOL]]
- [[Fully-Discrete-MOL-Convergence]]

### Chapter 10 — Convection-Diffusion
- [[Convection-Diffusion-Modeling]]
- [[Singular-Perturbation]]
- [[Upwind-Quadrature]]
- [[Streamline-Diffusion]]
- [[MOL-Convection-Diffusion]]

### Chapter 12 — Stokes Equations
- [[Stokes-Modeling]]
- [[Stokes-Constrained-Variational]]
- [[Stokes-Saddle-Point]]
- [[LBB-Condition]]
- [[Pressure-Instability]]
- [[Taylor-Hood-FEM]]
- [[Crouzeix-Raviart-FEM]]

### Chapter 13 — Finite Element Exterior Calculus
- [[Differential-Forms]]
- [[Exterior-Derivative-and-de-Rham-Complex]]
- [[Sobolev-Spaces-of-Forms]]
- [[Cochain-Calculus]]
- [[Discrete-Exterior-Derivative]]
- [[Whitney-Forms]]
- [[Electromagnetic-Wave-Equations]]
- [[Magnetostatics-Scalar-Potential]]
- [[Magnetostatics-Vector-Potential]]
- [[Magnetostatics-Saddle-Point-LBB]]

---

## Problem Cards (by theme)

### Chapter 1 — Elliptic BVPs
- [[Elliptic-BVP-Theory-Problems]] — Problems 1-1 through 1-11: quadratic functionals, Sobolev norms, variational formulations, BCs, strong ↔ weak form

### Chapter 2 — Finite Element Methods
- [[FEM-1D-2D-Problems]] — Problems 2-1 through 2-5, 2-10, 2-11, 2-16, 2-19, 2-23: Galerkin theory, element matrices, 1D/2D FEM
- [[FEM-Assembly-Implementation-Problems]] — Problems 2-6 through 2-9, 2-12 through 2-15, 2-17, 2-18, 2-20, 2-21, 2-22, 2-24: LehrFEM++ assembly, mesh, DOFs, BCs, parametric FEM

### Chapter 9 — Parabolic IBVPs
- [[Parabolic-Timestepping-Problems]] — Problems 9-1, 9-2, 9-3, 9-11, 9-14, 9-17, 9-20, 9-21, 9-22, 9-23

### Chapter 3 — FEM Convergence
- [[FEM-Error-Analysis-Problems]] — Problems 3-1, 3-2, 3-5, 3-6, 3-8, 3-11, 3-12, 3-13, 3-14, 3-15, 3-19, 3-21: a priori estimates, convergence rates, output functionals, duality
- [[FEM-Extensions-Advanced-Problems]] — Problems 3-3, 3-4, 3-7, 3-10, 3-16, 3-20, 3-22, 3-23, 3-24: non-standard formulations, maximum principle, parametric FE
- [[A-Posteriori-Error-Estimation-Problems]] — Problems 3-9, 3-17, 3-18: ZZ, residual-based, hierarchical error estimators

### Chapter 10 — Convection-Diffusion
- [[Convection-Diffusion-Problems]] — Problems 10-1, 10-2, 10-6, 10-7, 10-8

### Chapter 12 — Stokes
- [[Stokes-Problems]] — Problems 12-1, 12-2, 12-3, 12-4, 12-5

### Chapter 13 — FEEC
- [[FEEC-EM-Waves-Problems]] — Problems 13-1, 13-4
- [[Magnetostatics-Problems]] — Problems 13-2, 13-3

---

## Code Cards (LehrFEM++)
- [[LehrFEM-Assembly-Patterns]] — Full pipeline, element providers, COOMatrix, codim convention
- [[LehrFEM-Mesh-Patterns]] — Entity iteration, boundary detection, DOFs, Jacobian, VTK output
- [[LehrFEM-Solver-Convergence-Patterns]] — Sparse solvers, implicit Euler, SDIRK-2, convergence studies, quadrature
- [[LehrFEM-Convection-Patterns]] — `ConvBLFMatrixProvider`, upwind quadrature, SUPG stabilization
- [[LehrFEM-Stokes-Patterns]] — Mixed spaces, block system, Taylor-Hood DOFs, pressure pinning
- [[LehrFEM-FEEC-Patterns]] — Incidence operators, Whitney spaces, Maxwell/magnetostatics blocks

---

## Formula Reference
- [[Formulas-Sobolev-Norms]]
- [[Formulas-FEM-Assembly]]
- [[Formulas-Error-Estimates]]
- [[Formulas-Timestepping]]
- [[Formulas-Convection-Diffusion]]
- [[Formulas-Stokes]]
- [[Formulas-Exterior-Calculus]]

