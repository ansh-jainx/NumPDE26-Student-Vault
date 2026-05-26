---
tags: [exam, exam-critical, patterns]
---

# Exam Recurring Patterns — Full Course

Frequency matrix across **all 30 exam PDFs** (75 problems). Use with [[Exam-Master-Bank]] and theme deep dives.

Counts follow the same theme tags as [[Exam-Master-Bank]] (some problems match multiple study themes; the table uses a primary theme per row).

---

## Top recurring themes

| Theme | Count | Typical slot | Deep dive | Closest HW |
|-------|-------|--------------|-----------|------------|
| Elliptic weak form | 6+ midterm 0-1 chain | Midterm 0-1 | [[Exam-Deep-Elliptic-Weak-Form]] | 1-9, 1-10, 1-11 |
| Convection / upwind | 8 | Midterm 0-3, Endterm 0-2, finals SUPG | [[Exam-Deep-Convection-Upwind]] | 2-17, 10-8 |
| Parabolic / MOL | 11 | Endterm 0-1/0-2/0-3, finals heat | [[Exam-Deep-Parabolic-MOL]] | 9-17, 9-20, 9-11 |
| Stokes mixed | 4 | Endterm 0-1, finals 1-x | [[Exam-Deep-Stokes-Mixed]] | 12-1…12-5 |
| Convergence plots | 4 | Midterm 0-2, Endterm 0-1 | [[Exam-Deep-Convergence-Plots]] | 3-15, 3-19 |
| Element matrices | 2–3 | Midterm 0-2 | [[Exam-Deep-Element-Matrices]] | 2-13, 2-19 |
| FEEC / Maxwell | 2 | 2025 Summer 1-3 | [[Exam-Deep-FEEC-Maxwell]] | 13-3, 13-4 |
| RK theory (Ch.7) | 3 | Endterm 0-1/0-2 (2021–2022) | — | §7.3.3 |
| Legacy FVM / conservation | Tier C | 2018–2019 finals | — | out of week scope |

---

## If you only revise five topics

> [!danger] EXAM: minimum viable revision
> 1. **Midterm 0-1 elliptic chain** — Type A/B weak form, essential vs natural BCs ([[Exam-Deep-Elliptic-Weak-Form]])
> 2. **Endterm parabolic MOL + SDIRK** — [[Endterm-Ch9-Exam-Compendium]] (2024 0-1 boundary mass, 2025 0-2 SDIRK)
> 3. **Endterm Stokes theory** — [[Endterm-Ch12-Exam-Compendium]] (2025 0-1 LBB, rates)
> 4. **Convection upwind** — 2024 Endterm 0-2 `TransportUpwindQuadrature` ([[Exam-Deep-Convection-Upwind]])
> 5. **Convergence rate identification** — log-log slopes ([[Exam-Deep-Convergence-Plots]])

Add **finals coding** only if your exam includes Problem 1-x: Stokes or FEEC ([[Finals-Compendium]]).

---

## By exam type

### Midterm patterns (2021–2026)
| Slot | Recurrence | Notes |
|------|------------|-------|
| **0-1** | Elliptic BVP ↔ variational | Almost every year; mixed BC variants |
| **0-2** | Convergence **or** element matrix / criss-cross | 2021 convergence; 2023 criss-cross; 2026 curved triangle |
| **0-3** | Convection BLF **or** DOFHandler / quadratic FEM | Assembly literacy |

Full list: [[Midterm-Compendium]].

### Endterm patterns (2021–2025)
| Slot | Recurrence | Notes |
|------|------------|-------|
| **0-1** | Ch.9 parabolic **or** Ch.12 Stokes (2025) | 2024 parabolic evolution; 2025 Stokes theory |
| **0-2** | RK theory **or** upwind (2024) **or** SDIRK (2025) | Check year in [[Exam-Master-Bank#Ch9]] |
| **0-3** | Implicit RK / Radau parabolic | 2021, 2023 |

Submodule: [[Endterm-Recurring-Patterns]] (Ch.9+12 detail).

### Finals patterns (2019–2025)
| Slot | Recurrence | Notes |
|------|------------|-------|
| **1-1** | Parabolic coding (Gauss-Lobatto, MagDiff, BlackBody) | See [[Finals-Compendium]] |
| **1-2** | Stokes implementation (MINI, stab P1, pipe flow) | Folder names differ from endterm |
| **1-3** | Taylor-Hood **or** FEEC (2025) | 2024 Summer: `TaylorHoodNonMonolithic` |

---

## Chapter heat map

| Chapter | Exam weight | Primary weeks |
|---------|-------------|---------------|
| Ch.1 | HIGH (midterm) | [[Week-01-Elliptic-BVPs-I]], [[Week-02-Elliptic-BVPs-II]] |
| Ch.2 | HIGH (midterm + finals assembly) | [[Week-03-FEM-I]], [[Week-04-FEM-II]] |
| Ch.3 | MEDIUM (midterm + endterm plots) | [[Week-05-Parametric-FEM-and-Error]], [[Week-06-Convergence-and-Accuracy]] |
| Ch.7 | LOW (RK background) | [[Week-07-Parabolic-IBVPs]] |
| Ch.9 | HIGH (endterm + finals) | [[Week-07-Parabolic-IBVPs]] |
| Ch.10 | MEDIUM (2024 endterm) | [[Week-08-Convection-Diffusion]] |
| Ch.12 | HIGH (endterm + finals) | [[Week-09-Stokes-I]], [[Week-10-Stokes-II]] |
| Ch.13 | EMERGING (2025 finals) | [[Week-11-FEEC-I]] … [[Week-13-FEEC-Magnetostatics]] |

---

## Cross-links

- Problem-type recipes (full course): [[Exam-Problem-Types-Full-Course]]
- Endterm-only recipes: [[Endterm-Problem-Types-Recipes]]
- Folder reconciliation: [[Exam-Folder-Crosswalk]]
