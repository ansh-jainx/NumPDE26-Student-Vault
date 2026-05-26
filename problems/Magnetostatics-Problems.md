---
tags: [problems, chapter-13, FEEC, magnetostatics, saddle-point]
---

# Magnetostatics Problems

Problems from Chapter 13 covering Hodge-Laplacian, Whitney FEM, and stable saddle-point formulations for magnetostatics.

---

## Problem 13-2: Mixed FEM for the 2D Hodge-Laplacian

**Code folder:** `HodgeLaplacian2D` | **Sections:** §13.2.2, §13.3.3

**Concepts:** [[Whitney-Forms]], [[Magnetostatics-Vector-Potential]], [[Magnetostatics-Saddle-Point-LBB]]

**Setup:** Mixed finite element formulation of a Hodge-Laplacian model, emphasizing compatible FE spaces and block structure.

| Sub-task | What it asks |
|----------|--------------|
| (a) | Derive mixed weak formulation |
| (b) | Identify compatible primal/dual FE spaces |
| (c) | Assemble block operators and solve |

> [!abstract] Solution gist
> Write coupled equations in FEEC form language, discretize with Whitney-compatible spaces, and solve the resulting mixed linear system with appropriate null-space handling.

> [!warning] Common mistake
> Using incompatible trial/test spaces breaks commuting structure and can violate discrete inf-sup conditions.

---

## Problem 13-3: Whitney Finite Elements for Magnetostatic BVP in Two Dimensions

**Code folder:** `MagStat2D` | **Sections:** §13.3.3.1–§13.3.3.4

> NPDERepo path: `developers/MagStat2D/mysolution/`

**Concepts:** [[Magnetostatics-Scalar-Potential]], [[Magnetostatics-Vector-Potential]], [[Magnetostatics-Saddle-Point-LBB]], [[LBB-Condition]]

> [!warning] Exam alert
> **2025 Summer Final 1-3** (`MagStat2D`). Deep dive: [[Exam-Deep-FEEC-Maxwell]].

**Setup:** Magnetostatic boundary value problem in 2D with Whitney finite elements; compare potential-based formulations and discuss discrete LBB stability.

| Sub-task | What it asks |
|----------|--------------|
| (a) | Formulate scalar-potential and vector-potential variants |
| (b) | Explain gauge freedom and constraints |
| (c) | Build saddle-point system and verify stability assumptions |
| (d+) | Compute FE approximation and assess convergence |

> [!abstract] Solution gist
> Scalar potential gives a simpler elliptic baseline; vector potential gives physically structured FEEC model. Stable discretization requires compatibility and discrete LBB for mixed/gauge-constrained formulations.

> [!warning] Common mistake
> Ignoring gauge constraints leads to singular matrices and ambiguous magnetic potentials.

---

**Related concepts:** [[Magnetostatics-Scalar-Potential]], [[Magnetostatics-Vector-Potential]], [[Magnetostatics-Saddle-Point-LBB]], [[Whitney-Forms]], [[Formulas-Exterior-Calculus]], [[LehrFEM-FEEC-Patterns]]

**Cross-chapter:** Compare mixed saddle-point structure with [[Stokes-Saddle-Point]] and [[LBB-Condition]] from weeks 9–10.
