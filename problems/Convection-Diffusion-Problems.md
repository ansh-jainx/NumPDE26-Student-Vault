---
tags: [problems, chapter-10, convection-diffusion, upwind, SUPG]
---

# Convection-Diffusion Problems

Problems from Chapter 10 covering §10.1–§10.3.1: modeling, singular perturbation, upwind quadrature, streamline diffusion, MOL for transient convection-diffusion.

---

## Problem 10-1: Exponentially Fitted Upwind Scheme

**Code folder:** `ExpFittedUpwind` | **Sections:** §10.1.2, §10.2.2

**Concepts:** [[Convection-Diffusion-Modeling]], [[Singular-Perturbation]], [[Upwind-Quadrature]]

**Setup:** Semiconductor drift-diffusion model: $-\Delta u + u\,\nabla\Psi = f$ with exponential transformation $w = e^{-\Psi}u$. Derive variational form, element matrices with exponentially fitted flux, verify discrete maximum principle.

| What it tests |
|--------------|
| Convection-diffusion from physical conservation law |
| Exponential transformation for stability |
| Custom element matrix assembly |

> [!abstract] Solution gist
> **(a–c)** Transform: $w = e^{-\Psi}u$ linearizes convection → standard Laplacian form for $w$. **(d)** Lax-Milgram on transformed problem. **(e–f)** Integration by parts on triangles gives flux-based element matrices instead of standard stiffness. **(g+)** Exponentially fitted coefficients along edges → M-matrix structure → discrete maximum principle.

---

## Problem 10-2: Upwind Quadrature Method

**Code folder:** `UpwindQuadrature` | **Sections:** §10.2.1, §10.2.2.1

**Concepts:** [[Upwind-Quadrature]], [[Singular-Perturbation]], [[Convection-Diffusion-Modeling]]

> [!warning] Exam alert
> **2024 Endterm 0-2** maps primarily to Problem **10-8** (repo folder `UpwindQuadrature`; problem PDF naming often uses transport/upwind wording). Problem 10-2 is closely related practice on the same upwind idea.

**Setup:** Stationary convection-diffusion on unit square with $\varepsilon \ll 1$, constant velocity. Implement upwind quadrature FEM; compare with standard Galerkin for small $\varepsilon$.

| What it tests |
|--------------|
| Upwind quadrature on triangles |
| Stability for $\varepsilon \to 0$ |
| Layer resolution along flow direction |

> [!abstract] Solution gist
> **(a)** Weak form: $\varepsilon\int\nabla u\cdot\nabla v + \int(\mathbf{v}\cdot\nabla u)v = \int fv$. **(b–d)** Identify upstream node per triangle from $\mathbf{v}\cdot\mathbf{n}_i$. **(e+)** Implement in LehrFEM++; upwind scheme stable (no oscillations), standard Galerkin oscillates for $\varepsilon = 10^{-10}$.

---

## Problem 10-6: Streamline Upwind Method for Pure Advection Problem

**Code folder:** `AdvectionSUPG` | **Sections:** §10.2.2.2

**Concepts:** [[Streamline-Diffusion]], [[Singular-Perturbation]]

**Setup:** Pure advection $\mathbf{v}\cdot\nabla u = f$ (or $\varepsilon$ very small). Implement SUPG stabilization; test on 1D and 2D problems with known solutions.

| What it tests |
|--------------|
| SUPG parameter $\tau_K$ |
| Elimination of spurious oscillations |
| Convergence in $L^2$ |

> [!abstract] Solution gist
> Add $\tau_K\int_K (\mathbf{v}\cdot\nabla u)(\mathbf{v}\cdot\nabla v)$ to bilinear form. Choose $\tau_K \sim h_K/\|\mathbf{v}\|_K$. Compare with upwind and standard Galerkin on boundary layer test case.

---

## Problem 10-7: Streamline-Upwind Stabilized Finite Element Method

**Code folder:** `SUFEM` | **Sections:** §10.2.2.2

**Concepts:** [[Streamline-Diffusion]], [[Convection-Diffusion-Modeling]], [[LehrFEM-Convection-Patterns]]

**Setup:** Full convection-diffusion with SUPG on 2D mesh. Convergence study in $h$; compare $L^2$ and $H^1$ errors with/without stabilization.

| What it tests |
|--------------|
| Full SUPG pipeline in LehrFEM++ |
| Optimal convergence when layers resolved |
| Parameter sensitivity |

> [!abstract] Solution gist
> Extend 10-6 to 2D with diffusion + convection. SUPG preserves $O(h^2)$ $L^2$ convergence on smooth problems while stabilizing advection-dominated regime.

---

## Problem 10-8: Upwind Quadrature Scheme for Transport

**Code folder:** `UpwindQuadrature` | **Sections:** §10.2.2.1

> Exam solutions sometimes label this problem `TransportUpwindQuadrature` — same homework folder in NPDERepo.

**Concepts:** [[Upwind-Quadrature]], [[Convection-Diffusion-Modeling]]

> [!warning] Exam alert
> **2024 Endterm 0-2** (`TransportUpwindQuadrature`). Deep dive: [[Exam-Deep-Convection-Upwind#2024 Endterm 0-2 — Upwind quadrature]].

**Setup:** Transport-dominated problem on general mesh. Upwind quadrature + convergence study.

| What it tests |
|--------------|
| Upwind on non-Delaunay meshes |
| Transport vs convection-diffusion formulation |

> [!abstract] Solution gist
> Similar to 10-2 but emphasizes transport formulation and mesh generality. Verify first-order convergence in layer region, stability for large Peclet.

---

**Related concepts:** [[Convection-Diffusion-Modeling]], [[Singular-Perturbation]], [[Upwind-Quadrature]], [[Streamline-Diffusion]], [[MOL-Convection-Diffusion]], [[Formulas-Convection-Diffusion]], [[LehrFEM-Convection-Patterns]]

**Cross-chapter:** Problem **2-17** (`ConvBLFMatrixProvider`) — continuous convection form before upwind modification.
