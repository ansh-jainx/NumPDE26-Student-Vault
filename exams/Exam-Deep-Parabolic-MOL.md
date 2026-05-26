---
tags: [exam, exam-critical, chapter-9, deep-dive]
---

# Exam Deep Dive — Parabolic MOL & Timestepping

**Theme:** Parabolic evolution, MOL, implicit RK / SDIRK (10×) | **Types B/C/D/F**

> [!tip] Endterm detail already written
> For **2021–2025 endterm** walkthroughs, use [[Endterm-Ch9-Exam-Compendium]] — this file adds **full-course context** and **finals** without duplicating endterm prose.

> Master bank: [[Exam-Master-Bank#Ch9]] | Endterm hub: [[Endterm-Prep-Ch9-Ch12]]

---

## Anchor map

| Source | Document |
|--------|----------|
| Endterm 2025 0-2 SDIRK | [[Endterm-Ch9-Exam-Compendium#2025 Endterm 0-2 — MOL with SDIRK timestepping]] |
| Endterm 2024 0-1 boundary mass | [[Endterm-Ch9-Exam-Compendium#2024 Endterm 0-1 — Scalar parabolic evolution]] |
| Endterm 2023 0-3 Radau | [[Endterm-Ch9-Exam-Compendium#2023 Endterm 0-3 — Two-step Radau RK for heat]] |
| Endterm 2022 0-2/0-3 | [[Endterm-Ch9-Exam-Compendium]] |
| Endterm 2021 0-3 | [[Endterm-Ch9-Exam-Compendium#2021 Endterm 0-3 — 2-stage implicit RK parabolic timestepping]] |

---

## Finals-only anchors (coding)

| Folder | HW | Exam appearance | Strategy |
|--------|-----|-----------------|----------|
| `GaussLobattoParabolic` | 9-11 | 2023+ finals | Lobatto quadrature in mass matrix |
| `MagDiffWire` | 9-21 | finals | Magnetic diffusion MOL |
| `BlackBodyRadiation` | 9-22 | 2022 Winter | Nonlinear radiation BC |
| `RadauThreeTimestepping` | 9-1 | finals | Radau-3 implementation |
| `SDIRKMethodOfLines` | 9-2 | finals | MOL + SDIRK template |

See [[Finals-Compendium]] and [[Exam-Folder-Crosswalk]].

---

## Cross-cutting MOL recipe (Type C + D)

> [!example] HOW TO: Any parabolic MOL exam problem
> 1. **Spatial form:** $m(\dot{u},v) + a(u,v) = \ell(v)$ — identify $m$, $a$ (watch **boundary** mass in 2024 0-1).
> 2. **Semidiscrete:** $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$.
> 3. **Timestep:** Implicit Euler / SDIRK-2 / Radau — write stage equations with $\mathbf{M} + \tau\zeta\mathbf{A}$.
> 4. **Convergence:** Meta-Thm **9.2.8.5** — $O(h^p + \tau^q)$.

---

## Common folder-name mistakes

| Wrong | Correct |
|-------|---------|
| `SobolevEvolutionProblem` for 9-17 | `ParabolicEvolutionAspects` |
| Repo folder `MOLSDIRK` | NPDERepo **`SDIRK`** (HW 9-20) |

Details: [[Exam-Folder-Crosswalk]].

---

## Links

- Week: [[Week-07-Parabolic-IBVPs]]
- Problems: [[Parabolic-Timestepping-Problems]]
- Code: [[LehrFEM-Solver-Convergence-Patterns]]
- Formulas: [[Formulas-Timestepping]]
