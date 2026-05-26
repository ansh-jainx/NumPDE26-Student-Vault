---
tags: [exam, exam-critical, chapter-10, deep-dive]
---

# Exam Deep Dive — Convection & Upwind

**Theme:** Convection bilinear form + upwind quadrature (8×) | **Types C/G** | **HW:** 2-17, 10-8

> Master bank: [[Exam-Master-Bank#Ch10]] | Week: [[Week-08-Convection-Diffusion]]

---

## Anchor exams

| Year | Exam | Problem | Topic | Folder | HW |
|------|------|---------|-------|--------|-----|
| 2024 | Endterm | 0-2 | Upwind quadrature for transport | `TransportUpwindQuadrature` | 10-8 |
| 2024 | Midterm | 0-1 | Galerkin convection BLF | `ConvectionBilinearForm` | 2-17 |
| 2022 | Midterm | 0-2 | Advection BLF | — | 2-17 |
| 2021 | Midterm | 0-3 | Local convection computations | — | 2-17 |

Finals: `AdvectionSUPG` (10-6) — streamline diffusion; see [[Finals-Compendium]].

---

## 2024 Endterm 0-2 — Upwind quadrature

> [!danger] EXAM: Endterm scope exception
> Ch.10 appears on **2024 Endterm 0-2** even though endterm scope is Ch.9+12. Full walkthrough also in endterm recurring patterns.

**Folder:** `TransportUpwindQuadrature` (exam PDF) | **HW:** **10-8** | **Repo:** `homeworks/UpwindQuadrature`

**Strategy:**
1. Weak form with advection term $\int \mathbf{b}\cdot\nabla u\, v$.
2. Upwind quadrature: evaluate flux at upstream point based on sign of $\mathbf{b}\cdot\mathbf{n}$.
3. Local element matrices; non-symmetric structure.
4. Compare to naive Galerkin instability (oscillations at high Péclet).

**Code:** [[LehrFEM-Solver-Convergence-Patterns]], problem card [[Convection-Diffusion-Problems#Problem 10-8]].

---

## 2024 Midterm 0-1 — Convection bilinear form

**Type C** | Folder: `ConvectionBilinearForm` (exam PDF) → NPDERepo: `homeworks/ConvBLFMatrixProvider`

**Strategy:**
1. Local matrix $A_{ij}^K = \int_K \mathbf{b}\cdot\nabla\phi_j\,\phi_i\,\mathrm{d}x$.
2. No symmetry; assembly like diffusion but different gradient/test pairing.
3. Reference element quadrature on $\widehat{K}$.

**HW template:** Problem **2-17** (`ConvBLFMatrixProvider`).

---

## SUPG finals variant

**Folder:** `AdvectionSUPG` | HW **10-6**

Add stabilization $\tau_K \int_K \mathbf{b}\cdot\nabla u\,\mathbf{b}\cdot\nabla v$ — Type G implementation.

---

## Common mistakes

- Using symmetric assembly assumptions for convection.
- Wrong upwind direction (check $\mathbf{b}\cdot\mathbf{n}$ sign on each face).
- Confusing **10-8** (`TransportUpwindQuadrature`) with **10-2** (related transport HW).

---

## Links

- [[Exam-Deep-Element-Matrices]] (local computation skills)
- [[Upwind-Quadrature]] (concept)
- [[Convection-Diffusion-Problems]]
