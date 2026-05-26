---
tags: [exam, exam-critical, reference]
---

# Exam Folder Crosswalk

Maps **exam PDF code folders** → **homework problem id** → **NPDERepo clone path**. Extends [[Endterm-Scope-and-Sources#Exam vs homework vs NPDERepo folder names]] to the full course.

Ground truth: exam solution PDFs + NPDERepo `homeworks/` / `developers/` (local clone under `questions/NPDERepo/`).

**Column legend:** *Exam/PDF folder* = name in exam solution PDF; *NPDERepo* = directory to `cd` into for `mysolution/`.

---

## Theory / exam write-ups (no NPDERepo homework folder)

| Exam folder | Exam appearance | Practice instead |
|-------------|-----------------|------------------|
| `ParabolicEvolutionAspects` | 2024 Endterm 0-1 | HW **9-17** (theory; no repo folder) |
| `MOLSDIRK` | 2025 Endterm 0-2 | HW **9-20** → clone **`homeworks/SDIRK`** |
| `StokesVPFEM` | 2025 Endterm 0-1 | HW **12-4** (theory; no repo folder) |

> [!warning] Common mistake
> `ParabolicEvolutionAspects` is **not** `SobolevEvolutionProblem` (that is HW **9-12**).

---

## Name mismatches (exam PDF ≠ repo folder name)

| Exam/PDF folder | NPDERepo clone path | HW id | Notes |
|-----------------|---------------------|-------|-------|
| `MOLSDIRK` | `homeworks/SDIRK` | 9-20 | Same mastersolution content |
| `ElementMatrixCurvedTriangle` | `homeworks/ParametricElementMatrices` | 2-13 | 2026 Midterm 0-2 |
| `ConvectionBilinearForm` | `homeworks/ConvBLFMatrixProvider` | 2-17 | Midterm / finals |
| `TransportUpwindQuadrature` | `homeworks/UpwindQuadrature` | 10-8 | 2024 Endterm 0-2 |
| `DOFHandlerAssembly` / `QuadLagrFEM` | `homeworks/LFPPDofHandling` | 2-20 | 2023/2026 midterm assembly |
| `TaylorHoodNonMonolithic` | `homeworks/TaylorHoodNonMonolithic` | 12-3 | 2024 Summer 1-3 — **not** `StokesPipeFlow` |
| `StokesStabP1FEM` | `developers/StokesStabP1FEM` | 12-5 | 2025 Summer 1-2 |
| `MagDiffWire` | `developers/MagDiffWire` | 9-21 | Finals parabolic |
| `BlackBodyRadiation` | `developers/BlackBodyRadiation` | 9-22 | Finals parabolic |

---

## By theme (verified anchors)

### Ch.1 — Elliptic

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `VPtoBVP` / `VP_BVP_MP` | 1-10 | *(theory — no coding folder in current PDF)* |

### Ch.2 — FEM assembly

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `ElementMatrixCurvedTriangle` | 2-13 | `homeworks/ParametricElementMatrices` |
| `FESpacesCrissCross` | 2-19 | *(theory — no repo folder)* |
| `DOFHandlerAssembly` / `QuadLagrFEM` | 2-20 | `homeworks/LFPPDofHandling` |
| `ConvectionBilinearForm` | 2-17 | `homeworks/ConvBLFMatrixProvider` |

### Ch.9 — Parabolic

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `GaussLobattoParabolic` | 9-11 | `homeworks/GaussLobattoParabolic` |
| `MagDiffWire` | 9-21 | `developers/MagDiffWire` |
| `BlackBodyRadiation` | 9-22 | `developers/BlackBodyRadiation` |
| `RadauThreeTimestepping` | 9-1 | `homeworks/RadauThreeTimestepping` |
| `SDIRKMethodOfLines` | 9-2 | `homeworks/SDIRKMethodOfLines` |

### Ch.10 — Convection

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `AdvectionSUPG` | 10-6 | `homeworks/AdvectionSUPG` |
| `TransportUpwindQuadrature` | 10-8 | `homeworks/UpwindQuadrature` |

### Ch.12 — Stokes

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `StokesPipeFlow` | 12-1 | `homeworks/StokesPipeFlow` |
| `StokesMINIElement` | 12-2 | `homeworks/StokesMINIElement` |
| `TaylorHoodNonMonolithic` | 12-3 | `homeworks/TaylorHoodNonMonolithic` |
| `StokesVPFEM` | 12-4 | *(theory / exam write-up)* |
| `StokesStabP1FEM` | 12-5 | `developers/StokesStabP1FEM` |

### Ch.13 — FEEC

| Exam/PDF folder | HW | NPDERepo clone path |
|-----------------|-----|---------------------|
| `MagStat2D` | 13-3 | `developers/MagStat2D` |
| `MaxwellEvlTM` | 13-4 | `developers/MaxwellEvlTM` |

---

## Legacy / Tier C (2018–2019)

Older finals may reference FVM shallow-water or conservation-law folders **not** in current week handouts. Listed in [[Exam-Master-Bank#Other]] with Tier **C** — verify PDF before coding.

---

## Workflow before cloning NPDERepo

1. Find exam row in [[Exam-Master-Bank]]
2. Confirm folder name in **exam PDF** (not lecture title)
3. Check this crosswalk for **NPDERepo clone path** (not exam PDF name alone)
4. Open matching `problems/` card for gist + [[LehrFEM-Assembly-Patterns]] (or relevant `code/LehrFEM-*` card)

