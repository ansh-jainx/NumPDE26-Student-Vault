---
tags: [exam, exam-critical, index]
---

# Exam Prep — Full Course

**Numerical Methods for PDEs (401-0674-00L)** | Midterm, endterm, and summer/winter finals (2018–2026)

> [!tip] Start here
> - **Midterm (Ch.1–3):** [[Midterm-Compendium]] → [[Exam-Deep-Elliptic-Weak-Form]], [[Exam-Deep-Convergence-Plots]]
> - **Endterm (Ch.9 + Ch.12):** [[Endterm-Prep-Ch9-Ch12]] — full endterm module (Ch.9 + Ch.12 only)
> - **Summer/winter finals (coding):** [[Finals-Compendium]] → Stokes / FEEC / parabolic folders

---

## Story of the exams

Three exam formats recur across the semester. **Midterms** test elliptic theory (Ch.1), FEM assembly (Ch.2), and convergence literacy (Ch.3). **Endterms** (recent years) concentrate on **parabolic MOL + SDIRK** (Ch.9) and **Stokes saddle-point theory** (Ch.12). **Summer/winter finals** add **LehrFEM++ implementations**: Taylor-Hood, MINI, stabilized $P_1$–$P_1$, Gauss-Lobatto heat, magnetic diffusion, and (2025) **FEEC magnetostatics + Maxwell TM**.

This module indexes **all 30 exam PDFs (~75 problems)** with a **tiered depth** policy: ~20 anchor problems have theme deep dives; the rest appear in the master bank and week tables.

---

## Document map

### Foundation
| Document | Purpose |
|----------|---------|
| [[Exam-Master-Bank]] | Searchable table — every exam problem |
| [[Exam-Recurring-Patterns-Global]] | Frequency matrix; “if you only revise X” |
| [[Exam-Folder-Crosswalk]] | Exam PDF folder ↔ HW ↔ NPDERepo |
| [[Exam-Problem-Types-Full-Course]] | Types A–G + midterm-specific workflows |
| [[Exam-Manifest]] | Short overview of the exam index fields |

### By exam type
| Document | Scope |
|----------|---------|
| [[Midterm-Compendium]] | Midterms 2021–2026 (Ch.1–3 + occasional Ch.2 assembly) |
| [[Finals-Compendium]] | Summer/winter finals 2019–2025 (coding-heavy) |
| [[Endterm-Prep-Ch9-Ch12]] | Endterms 2021–2025 (Ch.9 + Ch.12 only) |

### Tier A — theme deep dives
| Theme | File | Recurrence |
|-------|------|------------|
| Elliptic weak form | [[Exam-Deep-Elliptic-Weak-Form]] | Midterm 0-1 (7×) |
| Convection / upwind | [[Exam-Deep-Convection-Upwind]] | 8× (midterm BLF + endterm upwind + SUPG finals) |
| Parabolic / MOL | [[Exam-Deep-Parabolic-MOL]] | 10× — **links to** [[Endterm-Ch9-Exam-Compendium]] |
| Stokes mixed | [[Exam-Deep-Stokes-Mixed]] | 4× — **links to** [[Endterm-Ch12-Exam-Compendium]] |
| Convergence plots | [[Exam-Deep-Convergence-Plots]] | 4× |
| Element matrices | [[Exam-Deep-Element-Matrices]] | 3× |
| FEEC / Maxwell | [[Exam-Deep-FEEC-Maxwell]] | 2× (2025 Summer) |

---

## Study paths

### Path A — Midterm in two weeks
1. [[Exam-Deep-Elliptic-Weak-Form]] + HW 1-9, 1-10, 1-11
2. [[Exam-Deep-Element-Matrices]] + HW 2-13, 2-19
3. [[Exam-Deep-Convergence-Plots]] + HW 3-15, 3-19
4. Skim [[Midterm-Compendium]] for remaining Tier B rows

### Path B — Endterm (Ch.9 + Ch.12)
Use [[Endterm-Prep-Ch9-Ch12]] exclusively for endterm scope. This hub only adds **cross-links** (e.g. 2024 Endterm 0-2 upwind → [[Exam-Deep-Convection-Upwind]]).

### Path C — Summer final (coding)
1. [[Finals-Compendium]] — pick your year's Problem 1-x folders
2. [[Exam-Folder-Crosswalk]] — verify NPDERepo paths before cloning
3. Code cards: [[LehrFEM-Stokes-Patterns]], [[LehrFEM-Solver-Convergence-Patterns]], [[LehrFEM-FEEC-Patterns]]

---

## Links to weekly material

Each week handout `## Exam Problems` table is synced from [[Exam-Master-Bank]]. Week → chapter map:

| Weeks | Chapters | Exam focus |
|-------|----------|------------|
| 1–2 | Ch.1 | Elliptic BVP ↔ variational form |
| 3–4 | Ch.2 | Element matrices, assembly, Lagrange FEM |
| 5–6 | Ch.3 | Convergence rates from data |
| 7 | Ch.7/9 | Parabolic IBVPs, RK background, MOL |
| 8 | Ch.10 | Convection BLF, upwind quadrature |
| 9–10 | Ch.12 | Stokes theory + stable pairs |
| 11–13 | Ch.13 | FEEC, Maxwell, magnetostatics (2025 finals) |

---

## Tier policy

| Tier | Count (approx.) | Treatment |
|------|-----------------|-----------|
| **A** | Theme anchors (~20 strategic) | Deep-dive MD + week link + problem alert |
| **B** | ~45 | Master bank + week table + problem alert |
| **C** | Legacy/rare | Master bank one-liner only |

Manifest tier counts may differ slightly from manual anchor counts; deep-dive files name **anchor exams** explicitly.

---

## Part of the vault graph

```
Exam-Prep-Index
├── Exam-Master-Bank
├── Midterm-Compendium / Finals-Compendium
├── Exam-Deep-* (7 themes)
└── Endterm-Prep-Ch9-Ch12 (existing submodule)
```

Home note: [[NumPDE — Numerical Methods for Partial Differential Equations]]
