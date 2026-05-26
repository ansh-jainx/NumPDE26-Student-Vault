---
tags: [endterm, exam-critical, reference]
---

# Endterm Scope and Sources

**Exam scope this term:** Chapter 9 (§9.2) + Chapter 12 (§12.1–§12.3.5) only.

---

## In scope

| Chapter | Script sections | Core topics |
|---------|-----------------|-------------|
| **9** | §9.2.1–§9.2.8 | Heat/parabolic IBVPs, spatial variational form, stability, MOL, implicit RK / SDIRK, stiffness, meta-theorem 9.2.8.5 |
| **12** | §12.1–§12.3.5 | Stokes modeling, saddle-point, LBB, pressure instability, Taylor-Hood, MINI, CR, stabilized $P_1$–$P_1$ |

## Out of scope (link only — do not revise for this endterm)

- **Chapter 10** — convection-diffusion (e.g. 2024 Endterm 0-2 upwind) → [[Week-08-Convection-Diffusion]]
- **Chapter 13** — FEEC / Maxwell → [[Week-11-FEEC-I]]
- **Midterms** — Ch.1–3 focus
- **Summer finals** — may include Stokes **coding** (Taylor-Hood, MINI, stabilized P1); endterm 2025 Stokes was **theory-only**

---

## PDF manifest

Place course PDFs and a clone of **NPDERepo** alongside this vault on your machine (paths vary by installation).

| File | Role |
|------|------|
| `NUMPDE.pdf` | Full lecture script (§9.2, §12) |
| `NPDEFL_Problems.pdf` | Homework statements + solutions (Ch.9: 9-1…9-23; Ch.12: 12-1…12-5) |
| `NPDE21_Endterm_sols.pdf` | Endterm 2021 solutions |
| `NPDE22_Endterm_sols.pdf` | Endterm 2022 solutions |
| `NPDE23_Endterm_sols.pdf` | Endterm 2023 solutions |
| `NPDE24_Endterm_sols.pdf` | Endterm 2024 solutions |
| `NPDE25_Endterm_sols.pdf` | Endterm 2025 solutions |
| `NPDE_Endterm_Spring_2018_sols.pdf` | Older endterm (Ch.9/12 index not applied to this PDF) |
| `NPDE_Endterm_Spring_2019_sols.pdf` | Older endterm |
| `questions/NPDERepo/` | C++ mastersolutions ground truth |

> [!warning] Missing locally
> Split script PDFs (`NUMPDE_till400.pdf`, etc.) and Hiptmair tablet notes (`NPDEVideo_*`) from course materials are **not** on disk. This module uses `NUMPDE.pdf` + existing week guides.

## Exam vs homework vs NPDERepo folder names

| Problem / exam | PDF / exam folder | NPDERepo `homeworks/` | Notes |
|----------------|-------------------|------------------------|-------|
| 9-17 / 2024 Endterm 0-1 | `ParabolicEvolutionAspects` | *(not in repo)* | Theory-only drill; **not** `SobolevEvolutionProblem` (that is **9-12**) |
| 9-20 / 2025 Endterm 0-2 | `MOLSDIRK` | `SDIRK` | Same problem content; repo uses shorter name |
| 2025 Endterm 0-1 Stokes | `StokesVPFEM` | *(not in repo)* | Exam-only; practice HW **12-4** (theory, no folder) |
| 12-5 / 2025 Summer 1-2 | `StokesStabP1FEM` | `developers/StokesStabP1FEM` | Summer final coding, not endterm |

---

## Endterm problem index (Ch.9 + Ch.12 only)

Verified against Endterm solution PDFs (2021–2025):

| Year | Problem | Title | Chapter | Closest HW |
|------|---------|-------|---------|------------|
| 2025 | 0-1 | FEM for Stokes BVPs | 12 | [[Stokes-Problems]] 12-4, 12-1, 12-3 |
| 2025 | 0-2 | MOL with SDIRK timestepping | 9 | 9-20 (`MOLSDIRK`; NPDERepo `SDIRK`) |
| 2024 | 0-1 | Scalar parabolic evolution (continuous & discrete) | 9 | 9-17 (`ParabolicEvolutionAspects`) |
| 2023 | 0-3 | Two-step Radau RK for heat | 9 | 9-14 |
| 2022 | 0-2 | RK single-step methods (general) | 9 | §7.3.3 + §9.2.7 |
| 2022 | 0-3 | Degenerate parabolic evolution | 9 | 9-17-style |
| 2021 | 0-3 | 2-stage implicit RK parabolic timestepping | 9 | 9-1 / Radau |
| 2021 | 0-1 | Embedded RK (Ch.7) | 9* | related RK theory |

\*2021 Problem 0-1 is primarily Ch.7 embedded RK; included as supplementary RK background.

Full walkthroughs: [[Endterm-Ch9-Exam-Compendium]], [[Endterm-Ch12-Exam-Compendium]].

---

## Standard theorem citations

| Result | Number |
|--------|--------|
| Poincaré–Friedrichs | 1.3.4.17 |
| Fundamental lemma | 1.5.3.4 |
| Green's formula | 1.5.2.7 |
| Céa's lemma | 3.1.3.7 |
| Interpolation error | 3.3.2.21 |
| Parabolic energy decay | Lemma 9.2.3.8 |
| MOL setup | §9.2.4 |
| SDIRK-2 example | Ex. 9.2.7.49 ($\zeta = 1 - \sqrt{2}/2$) |
| Fully discrete convergence | Meta-Thm 9.2.8.5 |
| LBB (Stokes) | Thm 12.2.2.23 |
| Stokes well-posedness | Thm 12.2.2.40 |
| Saddle-point Céa | Thm 12.3.3.13 |

---

## Source grounding

Content in this module is grounded in:

1. Endterm solution PDFs listed above
2. `NPDEFL_Problems.pdf` solutions
3. Week handouts and problem cards in this vault, cross-checked with NPDERepo folder names

Any step not directly visible in those sources is marked:

> [!warning] Note: interpretation — verify against PDF

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Recurring-Patterns]] | [[Endterm-Problem-Types-Recipes]]
