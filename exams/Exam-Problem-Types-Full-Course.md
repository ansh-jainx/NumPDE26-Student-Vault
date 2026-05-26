---
tags: [exam, exam-critical, recipes]
---

# Exam Problem Types — Full Course

Extends [[Endterm-Problem-Types-Recipes]] (Types A–G scoped to Ch.9/12) to **midterms, endterms, and finals**. Same letter taxonomy as the course standard.

---

## Type index

| Type | Name | Midterm | Endterm | Finals |
|------|------|---------|---------|--------|
| **A** | Derive weak form | ●●● | ●● | ● |
| **B** | Recover PDE from weak form | ●● | ●● | — |
| **C** | MOL / FEM matrix entries | ●● | ●●● | ●●● |
| **D** | Timestepping / RK tableau | ● | ●●● | ●● |
| **E** | Stability / inf-sup / LBB | ● | ●● | ● |
| **F** | Convergence rates / plots | ●● | ●● | ●● |
| **G** | Implementation / code structure | ● | — | ●●● |

Endterm detail: [[Endterm-Problem-Types-Recipes]].

---

## Midterm-specific workflows

### Type A — Elliptic weak form (Midterm 0-1)

> [!example] HOW TO: Midterm 0-1
> 1. Start from strong BVP: identify $-\nabla\cdot(\alpha\nabla u) + \beta u = f$.
> 2. Multiply by test $v$, integrate, IBP (Green 1.5.2.7).
> 3. Classify each boundary term → essential (eliminate) vs natural (retain).
> 4. State energy space ($H^1$, $H^1_0$, mixed Dirichlet/Neumann).
> 5. Optional: equivalent quadratic minimization (Thm 1.4.2.7).

**Anchors:** [[Exam-Deep-Elliptic-Weak-Form]] — 2026/2023/2022/2021 midterms.

### Type C — Local element matrix (Midterm 0-2)

> [!example] HOW TO: Element matrix on curved geometry
> 1. Reference element $(\widehat{K}, \widehat{V})$, Piola transforms for gradients.
> 2. Pull back $\int_K \nabla u \cdot \nabla v$ to reference quadrature.
> 3. Account for $|J|$ and metric from parametric map.
> 4. For convection BLF: $\int_K \mathbf{b}\cdot\nabla u\, v$ — not symmetric.

**Anchors:** [[Exam-Deep-Element-Matrices]], [[Exam-Deep-Convection-Upwind]].

### Type F — Convergence from data (Midterm 0-2 / Endterm 0-1)

> [!example] HOW TO: Identify order from log-log plot
> 1. Plot $\log(\text{error})$ vs $\log(h)$; slope ≈ convergence order.
> 2. Distinguish interpolation vs discretization error (parallel curves).
> 3. State expected order from $p$ and Sobolev index ($h^p$ for $H^1$ error).
> 4. Flag pollution / instability (flat or increasing error).

**Anchors:** [[Exam-Deep-Convergence-Plots]] — HW 3-15, 3-19.

---

## Endterm types (Ch.9 + Ch.12)

Use [[Endterm-Problem-Types-Recipes]] for step-by-step Ch.9/12 recipes. Cross-reference only:

| Endterm problem | Types used |
|-----------------|------------|
| 2025 0-1 Stokes | A, E (LBB), F (rates) |
| 2025 0-2 SDIRK | B, C, D, F |
| 2024 0-1 parabolic | C (boundary mass!), B, D |
| 2024 0-2 upwind | C, G (quadrature weights) |

---

## Finals types (coding)

### Type G — LehrFEM++ structure

> [!example] HOW TO: Finals Problem 1-x
> 1. Read exam PDF folder name → [[Exam-Folder-Crosswalk]]
> 2. Clone NPDERepo folder; compare `mastersolution/` structure
> 3. Identify: mesh factory, FE spaces, `AssembleMatrixLocally` codim, solver
> 4. For Stokes: block system or Schur complement; stable pair check
> 5. For FEEC: Whitney spaces, curl-curl mass, gauge fixing

**Anchors:** [[Finals-Compendium]], [[LehrFEM-Stokes-Patterns]], [[LehrFEM-FEEC-Patterns]].

---

## Quick routing

| You see… | Open |
|----------|------|
| “Reformulating elliptic variational problem” | [[Exam-Deep-Elliptic-Weak-Form]] |
| “Asymptotic convergence” / plots | [[Exam-Deep-Convergence-Plots]] |
| “Convection bilinear form” / upwind | [[Exam-Deep-Convection-Upwind]] |
| “Parabolic” / MOL / SDIRK / Radau | [[Exam-Deep-Parabolic-MOL]] → [[Endterm-Ch9-Exam-Compendium]] |
| “Stokes” / Taylor-Hood / MINI | [[Exam-Deep-Stokes-Mixed]] → [[Endterm-Ch12-Exam-Compendium]] |
| “Whitney” / magnetostatics / Maxwell | [[Exam-Deep-FEEC-Maxwell]] |

Master index: [[Exam-Master-Bank]].
