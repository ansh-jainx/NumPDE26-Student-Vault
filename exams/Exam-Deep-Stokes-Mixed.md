---
tags: [exam, exam-critical, chapter-12, deep-dive]
---

# Exam Deep Dive — Stokes Mixed FEM

**Theme:** Stokes saddle-point, stable pairs, finals coding (4×) | **Types A/C/E/G**

> [!tip] Endterm detail already written
> **2025 Endterm 0-1** full strategy: [[Endterm-Ch12-Exam-Compendium]] — this file links outward and covers **finals** implementations.

> Master bank: [[Exam-Master-Bank#Ch12]] | Endterm hub: [[Endterm-Prep-Ch9-Ch12]]

---

## Anchor map

| Year | Exam | Problem | Focus | Document |
|------|------|---------|-------|----------|
| 2025 | Endterm | 0-1 | Stokes theory (LBB, rates) | [[Endterm-Ch12-Exam-Compendium]] |
| 2024 | Summer | 1-3 | Taylor-Hood non-monolithic | below |
| 2024 | Winter | 1-3 | MINI element | below |
| 2025 | Summer | 1-2 | Stabilized P1–P1 | below |

---

## 2025 Endterm 0-1 — Theory (Type A/E/F)

**Folder:** `StokesVPFEM` *(theory / exam write-up)* | **HW practice:** **12-4**

Do **not** re-derive here — use [[Endterm-Ch12-Exam-Compendium]] and [[Endterm-Ch12-Student-Handout]].

Key exam facts: saddle-point (12.2.2.44), LBB Thm **12.2.2.23**, $S_2^0 \times S_0^{-1}$ rate, pressure instability of equal-order $P_1$–$P_1$.

---

## 2024 Summer 1-3 — Taylor-Hood non-monolithic

**Folder:** `TaylorHoodNonMonolithic` | **HW:** **12-3**

> [!warning] Folder name
> Exam PDF uses **`TaylorHoodNonMonolithic`**, not `StokesPipeFlow`.

**Strategy (Type G):**
1. $Q_2$ velocity / $P_1$ or $P_0$ pressure on simplex mesh.
2. Block system $\begin{pmatrix}\mathbf{A} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0}\end{pmatrix}$.
3. Inf-sup satisfied — no spurious pressure modes.
4. Non-monolithic: separate assembly passes or block preconditioner.

**Code:** [[LehrFEM-Stokes-Patterns]].

---

## 2024 Winter 1-3 — MINI element

**Folder:** `StokesMINIElement` | **HW:** **12-2**

Bubble-enriched velocity on triangle; pressure $P_1$; minimal DOF count for stability.

---

## 2025 Summer 1-2 — Stabilized $P_1$–$P_1$

**Folder:** `StokesStabP1FEM` | **HW:** **12-5** | **Repo:** `developers/StokesStabP1FEM`

Equal-order pair + stabilization — contrast with LBB-failure of unstabilized $P_1$–$P_1$ (2025 Endterm 0-1 theory).

---

## Other finals folders

| Folder | HW | Note |
|--------|-----|------|
| `StokesPipeFlow` | 12-1 | Channel geometry |
| `StokesVPFEM` | 12-4 | Variational Stokes (theory write-up; no NPDERepo folder) |

---

## Links

- Weeks: [[Week-09-Stokes-I]], [[Week-10-Stokes-II]]
- Problems: [[Stokes-Problems]]
- Concepts: [[LBB-Condition]], [[Taylor-Hood-FEM]], [[Pressure-Instability]]
- Finals index: [[Finals-Compendium]]
