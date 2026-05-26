---
tags: [exam, exam-critical, finals, exam-bank]
---

# Finals Compendium — Summer & Winter (2019–2025)

Tier **B** summaries for **Final** exam problems (Problem 1-x coding slots). Theory endterms are in [[Endterm-Prep-Ch9-Ch12]].

Sources: `NPDESpring20XX_Exam_Summer_sols.pdf`, `NPDESpring20XX_Exam_Winter_sols.pdf`, legacy 2018–2019 exams.

Folder crosswalk: [[Exam-Folder-Crosswalk]].

---

## Structure of finals

| Slot | Typical content | Chapter |
|------|-----------------|---------|
| **1-1** | Parabolic / heat MOL implementation | Ch.9 |
| **1-2** | Stokes stable element implementation | Ch.12 |
| **1-3** | Taylor-Hood non-monolithic **or** FEEC (2025) | Ch.12 / Ch.13 |

Problem 0-x on finals (when present) often mirrors midterm/endterm theory — see [[Exam-Master-Bank]].

---

## 2025 Summer Final

### 1-1 — (Parabolic / MOL — see PDF)
Check folder in exam PDF; likely Gauss-Lobatto or SDIRK variant. Cross-ref [[Exam-Deep-Parabolic-MOL]].

### 1-2 — Stabilized $P_1$–$P_1$ Stokes
**Folder:** `StokesStabP1FEM` | HW **12-5** | Repo: `developers/StokesStabP1FEM`

**Strategy:** Stabilization parameter; equal-order pressure-velocity; compare to Taylor-Hood inf-sup.

→ [[Exam-Deep-Stokes-Mixed#2025 Summer 1-2]]

### 1-3 — FEEC: magnetostatics + Maxwell TM
**Folders:** `MagStat2D`, `MaxwellEvlTM` | HW **13-3**, **13-4**

**Strategy:** Whitney forms; curl-curl problems; MOL for Maxwell; gauge / boundary conditions.

→ [[Exam-Deep-FEEC-Maxwell]]

---

## 2024 Summer Final

### 1-1 — (Parabolic coding — see PDF)
Often heat equation with specialized quadrature — compare [[Exam-Master-Bank#Ch9]].

### 1-3 — Taylor-Hood non-monolithic
**Folder:** `TaylorHoodNonMonolithic` | HW **12-3**

> [!warning] Not `StokesPipeFlow`
> 2024 Summer 1-3 uses **`TaylorHoodNonMonolithic`** per the exam solution PDF.

**Strategy:** Separate spaces $Q_2$ velocity / $P_0$ or $P_1$ pressure; Schur complement or block solver.

→ [[Exam-Deep-Stokes-Mixed]]

---

## 2024 Winter Final

### 1-3 — Stokes MINI element
**Folder:** `StokesMINIElement` | HW **12-2**

**Strategy:** MINI bubble enrichment; inf-sup on simplex; block assembly.

→ [[Exam-Deep-Stokes-Mixed]]

---

## 2023 Summer / Winter

Parabolic and Stokes coding problems — folders in [[Exam-Master-Bank#Ch9]] and [[Exam-Master-Bank#Ch12]]:

| Common folders | HW |
|----------------|-----|
| `GaussLobattoParabolic` | 9-11 |
| `MagDiffWire` | 9-21 |
| `StokesPipeFlow` | 12-1 |
| `AdvectionSUPG` | 10-6 |

**Strategy:** Clone matching NPDERepo folder; compare `mastersolution/main.cc` structure.

---

## 2022 Summer / Winter

- **`BlackBodyRadiation`** (9-22) — nonlinear radiation BC / MOL
- **`StokesPipeFlow`** (12-1) — channel flow geometry
- **`AdvectionSUPG`** (10-6) — streamline diffusion stabilization

→ [[Exam-Deep-Convection-Upwind]] (SUPG), [[Exam-Deep-Parabolic-MOL]] (BlackBody)

---

## 2021 Summer / Winter

Earlier Stokes / heat finals; see master bank rows for `StokesPipeFlow`, `RadauThreeTimestepping`, `SDIRKMethodOfLines`.

---

## 2019–2020 / 2018 (Tier C)

Legacy finals may include **FVM shallow water** or conservation laws (**out of week scope**). Entries marked Tier **C** in [[Exam-Master-Bank#Other]] — one-line index only.

---

## Coding checklist (Type G)

- [ ] Confirm exam PDF folder name → [[Exam-Folder-Crosswalk]]
- [ ] Open NPDERepo `mastersolution/` before writing `mysolution/`
- [ ] Stokes: verify stable pair (Taylor-Hood / MINI / stab P1)
- [ ] Parabolic: codim 0 vs 1 for mass / boundary terms
- [ ] FEEC: use [[LehrFEM-FEEC-Patterns]] for Whitney assembly

**Theory counterpart:** [[Endterm-Prep-Ch9-Ch12]] | **Midterm:** [[Midterm-Compendium]]
