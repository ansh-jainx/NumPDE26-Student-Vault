---
tags: [endterm, exam-critical, index]
---

# Endterm Prep — Ch.9 & Ch.12

**Numerical Methods for PDEs (401-0674-00L)** | Endterm preparation module

**Exam scope:** Chapter 9 (§9.2 parabolic evolution) + Chapter 12 (§12 Stokes FEM theory & stable pairs)

> Part of full-course exam prep: [[Exam-Prep-Index]] | Master bank: [[Exam-Master-Bank]]

---

## Story of the endterm

Two threads from the semester converge on the exam. **Chapter 9** asks: given a dissipative evolution PDE, write the spatial variational form, semidiscretize to $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$, and timestep with stiffly stable implicit RK — especially SDIRK-2. **Chapter 12** asks: given viscous incompressible flow, write the Stokes saddle-point form, assemble the block system, and explain why only certain mixed elements (Taylor-Hood, MINI, CR) are stable. Recent endterms (2024–2025) tested **theory**, not full LehrFEM implementations.

---

## Suggested study order (students)

| Step | Topic | Document |
|------|-------|----------|
| 1 | Ch.9 reference + self-check | [[Endterm-Ch9-Student-Handout]] |
| 2 | Ch.9 exam problems (2024, 2025) | [[Endterm-Ch9-Exam-Compendium]] |
| 3 | Ch.9 priority homework | [[Endterm-Ch9-Homework-Walkthrough]] |
| 4 | Ch.12 reference + self-check | [[Endterm-Ch12-Student-Handout]] |
| 5 | 2025 Stokes endterm deep dive | [[Endterm-Ch12-Exam-Compendium]] |
| 6 | Mixed practice | [[Endterm-Practice-Set]] |

---

## Document map

### Foundation
- [[Endterm-Scope-and-Sources]] — PDF manifest, in/out scope, theorem index
- [[Endterm-Recurring-Patterns]] — what repeats across 2021–2025 endterms
- [[Endterm-Problem-Types-Recipes]] — Types A–G step-by-step
- [[Exam-Folder-Crosswalk]] — exam PDF folder names ↔ NPDERepo paths

### Chapter 9 — Parabolic / MOL
| Document | Role |
|----------|------|
| [[Endterm-Ch9-Student-Handout]] | Condensed reference + self-check |
| [[Endterm-Ch9-Exam-Compendium]] | All Ch.9 endterm problems 2021–2025 |
| [[Endterm-Ch9-Homework-Walkthrough]] | Priority homework aligned with endterm |

### Chapter 12 — Stokes
| Document | Role |
|----------|------|
| [[Endterm-Ch12-Student-Handout]] | Condensed reference + self-check |
| [[Endterm-Ch12-Exam-Compendium]] | 2025 Stokes endterm deep dive |
| [[Endterm-Ch12-Homework-Walkthrough]] | Priority homework aligned with endterm |

### Practice & code
- [[Endterm-Code-Cheatsheet]] — MOL, SDIRK-2, Stokes block (NPDERepo-verified)
- [[Endterm-Practice-Set]] — mock questions with exam tags

---

## Links to weekly material

| Week | Handout | Endterm role |
|------|---------|--------------|
| 7 | [[Week-07-Parabolic-IBVPs]] | Ch.9 core theory |
| 9 | [[Week-09-Stokes-I]] | Ch.12 saddle-point, LBB |
| 10 | [[Week-10-Stokes-II]] | Stable pairs, Taylor-Hood |

| Problem cards | Code cards |
|---------------|------------|
| [[Parabolic-Timestepping-Problems]] | [[LehrFEM-Solver-Convergence-Patterns]] |
| [[Stokes-Problems]] | [[LehrFEM-Stokes-Patterns]] |

| Formulas |
|----------|
| [[Formulas-Timestepping]], [[Formulas-Stokes]] |

---

## Summary — exam priority

| Topic | Priority | Endterm evidence |
|-------|----------|------------------|
| Spatial variational form (parabolic) | **HIGH** | 2024 0-1 |
| MOL matrices $\mathbf{M}$, $\mathbf{A}$ | **HIGH** | 2024 0-1, 2025 0-2 |
| SDIRK-2 / implicit RK on MOL | **HIGH** | 2025 0-2, 2023 0-3 |
| Balanced refinement (9.2.8.5) | **MED** | 2025 0-2(d) |
| Stokes saddle-point weak form | **HIGH** | 2025 0-1 |
| Discrete LBB / stable pairs | **HIGH** | 2025 0-1 |
| Block system assembly | **MED** | 2025 0-1, HW 12-4 |
| Element matrix fill-in | **LOW** | HW-heavy |
| LehrFEM Stokes coding | **LOW** on endterm | summer finals |

---

## Master exam checklist

- [ ] Derive parabolic spatial form; locate BCs in $m$, $a$, $\ell$
- [ ] Write $\mathbf{M}$, $\mathbf{A}$ for given FEM space and bilinear forms
- [ ] Set up SDIRK-2 stages; explain decoupling vs Radau Kronecker
- [ ] State meta-theorem 9.2.8.5; balance $\tau$ and $h$
- [ ] Write Stokes saddle-point form (12.2.2.44); block matrix
- [ ] State LBB1 + LBB2; explain $P_1$–$P_1$ failure
- [ ] Name Taylor-Hood spaces and convergence rates

---

## Quick-fire review (mixed)

1. What is the MOL ODE for $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$?
2. Where does Robin BC $cu$ enter — $\mathbf{M}$ or $\mathbf{A}$?
3. SDIRK-2: how many linear solves per step with same factorization?
4. Why is $\lambda_{\max} = O(h^{-2})$ fatal for explicit Euler?
5. Strong form recovered from 2024 Endterm 0-1 variational form?
6. Write Stokes block system symbolically.
7. What is LBB2 in words?
8. Taylor-Hood local DOF count on one triangle (2D velocity+pressure)?
9. Meta-theorem error bound for $p=2$, $q=2$?
10. CR element: conforming or non-conforming velocity?

Answers in [[Endterm-Practice-Set#Self-check answers]].

---

**Start here for students:** [[Endterm-Ch9-Student-Handout]] + [[Endterm-Ch12-Student-Handout]]
