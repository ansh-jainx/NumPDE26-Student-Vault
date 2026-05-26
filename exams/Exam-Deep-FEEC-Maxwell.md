---
tags: [exam, exam-critical, chapter-13, deep-dive]
---

# Exam Deep Dive — FEEC & Maxwell

**Theme:** Magnetostatics + Maxwell TM modes (2025 finals) | **Types A/C/G** | **HW:** 13-3, 13-4

> Master bank: [[Exam-Master-Bank#Ch13]] | Weeks: [[Week-11-FEEC-I]], [[Week-12-FEEC-II-and-EM-Waves]], [[Week-13-FEEC-Magnetostatics]]

---

## Anchor exams (two separate finals)

> [!tip] Two exams, same problem number
> Both use slot **1-3** but on **different** PDFs (Summer vs Winter). Do not merge into one anchor.

### 2025 Summer Final 1-3 — MagStat2D

| Folder | HW | PDF |
|--------|-----|-----|
| `MagStat2D` | **13-3** | `NPDE_Spring2025_Exam_Summer_sols.pdf` |

### 2025 Winter Final 1-3 — MaxwellEvlTM

| Folder | HW | PDF |
|--------|-----|-----|
| `MaxwellEvlTM` | **13-4** | `NPDE_Spring2025_Exam_Winter_sols.pdf` |

---

## MagStat2D (HW 13-3) — Summer

**Strategy:**
1. Vector potential / field representation with Whitney 1-forms.
2. Curl-curl weak form: $\int (\text{curl}\,\mathbf{u})\cdot(\text{curl}\,\mathbf{v})$.
3. Gauge condition or divergence constraint handling.
4. Compare to Stokes saddle-point structure (LBB analogy) — [[Week-13-FEEC-Magnetostatics]].

**Repo:** `developers/MagStat2D` | Problems: [[Magnetostatics-Problems]].

---

## MaxwellEvlTM (HW 13-4) — Winter

**Strategy:**
1. TM mode reduction → scalar/vector wave equation in 2D.
2. Spatial FEEC discretization + MOL (link [[Method-of-Lines]]).
3. Whitney edge elements for curl-conforming fields.
4. Timestepping stability (CFL / implicit options per exam spec).

**Repo:** `developers/MaxwellEvlTM` | Problems: [[FEEC-EM-Waves-Problems]].

---

## FEEC exam vocabulary

| Term | Exam use |
|------|----------|
| Whitney forms | Edge/face DOFs on mesh |
| Curl-curl mass | Stiffness from $\text{curl}\,\mathbf{u}\cdot\text{curl}\,\mathbf{v}$ |
| de Rham complex | Exactness chain for stable discretization |
| LBB (discrete) | Inf-sup for mixed magnetostatic formulations |

Concepts: [[Whitney-Forms]], [[Cochain-Calculus]], [[Electromagnetic-Wave-Equations]].

---

## Code patterns

[[LehrFEM-FEEC-Patterns]] — implementation patterns; see NPDERepo `magstat2d.*`, `maxwellevltm.*`.

---

## Links

- [[Finals-Compendium#2025 Summer Final]]
- [[Exam-Folder-Crosswalk#Ch.13 — FEEC]]
- [[LBB-Condition]] (Stokes ↔ magnetostatics parallel)
