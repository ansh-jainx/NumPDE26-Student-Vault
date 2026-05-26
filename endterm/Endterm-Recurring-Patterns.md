---
tags: [endterm, exam-critical, analytics]
---

# Endterm Recurring Patterns (Ch.9 & Ch.12)

Frequency analysis over **Endterm exams 2021–2025** (Ch.9/12 problems only). Use this to prioritize revision time.

---

## Pattern frequency matrix

| Pattern | Appearances | Exam examples | Priority |
|---------|-------------|---------------|----------|
| **Implicit RK / SDIRK on MOL** | 5+ | 2025 0-2, 2023 0-3, 2021 0-3, 2022 0-2 | **HIGH** |
| **MOL matrix identification** ($\mathbf{M}$, $\mathbf{A}$) | 4+ | 2024 0-1, 2025 0-2, 2023 0-3 | **HIGH** |
| **Weak form derive / fill-in** | 4+ | 2024 0-1 (spatial), 2025 0-1 (Stokes) | **HIGH** |
| **Stokes saddle-point + block system** | 1 (recent) | 2025 0-1 | **HIGH** (only Ch.12 endterm in corpus) |
| **Recover strong PDE from weak form** | 2+ | 2024 0-1, 2022 0-3 | **MED** |
| **Balanced $h$–$\tau$ refinement** | 2+ | 2025 0-2, homework 9-20 | **MED** |
| **Stability / energy decay proof** | 2+ | 2022 0-3, HW 9-3 | **MED** |
| **Element matrix fill-in** | rare on endterm | more common midterm / HW | **LOW** |
| **LehrFEM code blanks** | rare on endterm | summer finals 2024–2025 | **LOW** (supplementary) |

---

## If you only revise five things

1. **Spatial variational form** for parabolic IBVP — identify $m$, $a$, $\ell$ and where BCs land ([[Spatial-Variational-Formulation-Parabolic]], [[Formulas-Timestepping]]).
2. **MOL ODE** $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$ — matrix entries from bilinear forms ([[Method-of-Lines]]).
3. **SDIRK-2 stage system** — multiply MOL by $\mathbf{M}$, two solves with $\mathbf{M} + \zeta\tau\mathbf{A}$ ([[Timestepping-MOL]], [[Endterm-Problem-Types-Recipes#Type D]]).
4. **Stokes saddle-point weak form** — $a$, $b$, pressure mean-zero / Lagrange multiplier ([[Stokes-Saddle-Point]], [[Formulas-Stokes]]).
5. **Stable mixed pairs + discrete LBB** — why $P_1$–$P_1$ fails; Taylor-Hood ([[Taylor-Hood-FEM]], [[Pressure-Instability]]).

---

## BC traps that repeat on exams

| BC type | Goes into | Typical mistake |
|---------|-----------|-----------------|
| Dirichlet $u = g$ | essential / $H^1_0$ trial space | putting BC in $\mathbf{A}$ instead of space |
| Neumann $\nabla u \cdot \mathbf{n} = h$ | natural (no boundary term in $a$) | adding spurious boundary integral |
| Robin $-\nabla u \cdot \mathbf{n} = c u$ | **edge integral in $a$** | putting Robin term in $\mathbf{M}$ |
| Boundary evolution $\dot{u}$ on $\partial\Omega$ | **boundary mass in $\mathbf{M}$** | using volume integral for $\mathbf{M}$ (2024 Endterm 0-1) |
| Weighted mass $\sigma(\mathbf{x})\dot{u}$ | volume mass with coefficient | forgetting $\sigma$ in $\mathbf{M}$ (2025 Endterm 0-2) |

---

## Exam ↔ homework crosswalk (highest yield)

| Endterm | HW drill |
|---------|----------|
| 2025 0-2 SDIRK | 9-20, 9-2 |
| 2024 0-1 boundary mass | 9-17 |
| 2023 0-3 Radau Kronecker | 9-14, 9-1 |
| 2025 0-1 Stokes theory | 12-4, 12-3 |
| 2022 0-3 degenerate parabolic | 9-17, 9-3 |

Details: [[Endterm-Ch9-Homework-Walkthrough]], [[Endterm-Ch12-Homework-Walkthrough]].

---

## What endterm is *not* (common student confusion)

- **Not** upwind / SUPG (Ch.10) — that was 2024 Endterm 0-2, out of scope this term
- **Not** Whitney forms / Maxwell (Ch.13)
- **Not** guaranteed to include LehrFEM implementation — 2025 endterm was theory for both Ch.9 and Ch.12
- Summer final **may** add Stokes coding (Taylor-Hood, MINI) — see [[Endterm-Code-Cheatsheet]] appendix

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Scope-and-Sources]] | [[Endterm-Problem-Types-Recipes]]
