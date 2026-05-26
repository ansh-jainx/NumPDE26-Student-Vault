---
tags: [problems, chapter-12, Stokes, Taylor-Hood, mixed-FEM]
---

# Stokes Problems

Problems from Chapter 12 covering §12.1–§12.3.5: Stokes modeling, saddle-point formulation, Taylor-Hood and MINI/CR elements, stabilized $P_1$–$P_1$.

---

## Problem 12-4: FEM for Stokes BVPs

**Code folder:** `—` | **Sections:** §12.2.2, §12.2.3, §12.3

**Concepts:** [[Stokes-Saddle-Point]], [[LBB-Condition]], [[Stokes-Modeling]]

> [!warning] Exam alert
> **Direct template for 2025 Endterm Problem 0-1** (40 pts). See [[Endterm-Ch12-Exam-Compendium]].

**Setup:** Theoretical — derive discrete saddle-point system for Stokes, identify bilinear forms $a$, $b$, block matrix structure. No heavy coding.

| What it tests |
|--------------|
| Saddle-point → block Galerkin system |
| Role of $a$ (viscous) and $b$ (divergence) |
| Pressure mean-zero constraint |

> [!abstract] Solution gist
> **(a)** Write $a(\mathbf{u},\mathbf{w}) = \int \mu D\mathbf{u}:D\mathbf{w}$, $b(\mathbf{w},q) = -\int q\,\mathrm{div}\,\mathbf{w}$. **(b)** Block system $(\mathbf{A}, \mathbf{B}^T; \mathbf{B}, \mathbf{0})$. **(c)** Pin pressure or impose $\int p_h = 0$ for uniqueness. **(d)** State discrete LBB requirement for stable pair.

---

## Problem 12-1: Viscous Flow Simulation with Taylor-Hood FEM

**Code folder:** `StokesPipeFlow` | **Sections:** §12.1, §12.3.4

**Concepts:** [[Taylor-Hood-FEM]], [[Stokes-Saddle-Point]], [[Stokes-Modeling]], [[LehrFEM-Stokes-Patterns]]

> [!warning] Exam alert
> Finals coding template (**2024 Summer** Taylor-Hood, etc.); **2025 Endterm 0-1** tests Stokes FEM at theory/assembly level only.

**Setup:** 2D pipe flow: Stokes with parabolic inlet/outlet profiles, no-slip walls. Taylor-Hood FEM, VTK output, power dissipation.

| Sub-task | What it asks |
|----------|-------------|
| (a) | Separation of variables: exact solution family for straight pipe |
| (b) | Fix outlet flux constant $v_0$ |
| (c) | Compute power dissipation $\int_\Omega |\mathrm{curl}\,\mathbf{v}|^2$ |
| (d+) | Implement Taylor-Hood in LehrFEM++, simulate flow |

> [!abstract] Solution gist
> **(a)** $\mathbf{v} = (v(x_2), 0)^T$, $p = p(x_1)$ → ODEs, parabolic velocity profile. **(b)** Mass flux balance fixes $v_0$. **(c)** $\mathrm{curl}\,\mathbf{v} = \partial v_1/\partial x_2$ for 2D. **(d+)** Block assembly, solve, visualize streamlines.

---

## Problem 12-2: The MINI Element for Stokes

**Code folder:** `StokesMINIElement` | **Sections:** §12.3.4

**Concepts:** [[Taylor-Hood-FEM]], [[Pressure-Instability]], [[LBB-Condition]]

**Setup:** MINI element: $P_1$ velocity + cubic bubble per cell + $P_1$ pressure. Another stable mixed pair.

| What it tests |
|--------------|
| Bubble enrichment of velocity space |
| Comparison with Taylor-Hood |

> [!abstract] Solution gist
> MINI adds local bubble functions to $P_1$ velocity → satisfies discrete LBB. Implementation parallels 12-1 with different local DOF structure.

---

## Problem 12-3: Taylor-Hood FEM for Stokes BVP

**Code folder:** `TaylorHoodNonMonolithic` | **Sections:** §12.3.4

**Concepts:** [[Taylor-Hood-FEM]], [[Stokes-Saddle-Point]], [[LehrFEM-Stokes-Patterns]]

**Setup:** Taylor-Hood on cavity/domain with manufactured solution. Non-monolithic solver; convergence rates.

| What it tests |
|--------------|
| $O(h^2)$ convergence for $\mathbf{u}$ and $p$ |
| Block solver strategies |

> [!abstract] Solution gist
> Manufactured $\mathbf{u}$, $p$ → compute $\mathbf{f}$ → solve → verify $\|\mathbf{u}-\mathbf{u}_h\|_{H^1}$, $\|p-p_h\|_{L^2} = O(h^2)$ on refinement sequence.

---

## Problem 12-5: Stabilized P1-FEM for Stokes

**Code folder:** `StokesStabP1FEM` | **Sections:** §12.3.1, §12.3.2

> NPDERepo path: `developers/StokesStabP1FEM/mysolution/`

**Concepts:** [[Pressure-Instability]], [[Taylor-Hood-FEM]], [[Stokes-Saddle-Point]]

**Setup:** Equal-order $P_1$–$P_1$ with stabilization (penalty/least-squares) instead of Taylor-Hood.

| What it tests |
|--------------|
| Why naive $P_1$–$P_1$ fails |
| Stabilization restores stability |

> [!abstract] Solution gist
> Naive $P_1$–$P_1$: pressure oscillations. Add stabilization term $\alpha\int (\mathrm{div}\,\mathbf{u}_h)(\mathrm{div}\,\mathbf{v}_h)$ or grad-div → stable but different accuracy than Taylor-Hood.

---

**Related concepts:** [[Stokes-Modeling]], [[Stokes-Constrained-Variational]], [[Stokes-Saddle-Point]], [[LBB-Condition]], [[Pressure-Instability]], [[Taylor-Hood-FEM]], [[Crouzeix-Raviart-FEM]], [[Formulas-Stokes]], [[LehrFEM-Stokes-Patterns]]

**Cross-chapter:** Problems **2-14**, **3-16** ([[Crouzeix-Raviart-FEM]]); Problem **2-22** (saddle-point preview with [[Stokes-Saddle-Point]]).

**Endterm prep:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Ch12-Exam-Compendium]] | [[Endterm-Ch12-Homework-Walkthrough]]
