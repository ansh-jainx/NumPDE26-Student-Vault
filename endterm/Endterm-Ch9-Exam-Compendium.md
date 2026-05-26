---
tags: [endterm, exam-critical, chapter-9, exam-bank]
---

# Endterm Ch.9 — Exam Compendium

Every **Endterm** problem (2021–2025) touching Chapter 9. Strategy only — full solutions in exam PDFs and homework walkthrough.

Sources: `NPDE21`–`NPDE25_Endterm_sols.pdf`. Crosswalk: [[Endterm-Recurring-Patterns]].

---

## 2025 Endterm 0-2 — MOL with SDIRK timestepping

**Folder (exam PDF):** `MOLSDIRK` | **NPDERepo:** `SDIRK` | **HW template:** Problem **9-20** | **Sections:** §9.2.2, §9.2.4, §9.2.7, §9.2.8 | **Points:** 15+10+20+15 = 60

**Setup (from exam PDF):** Parabolic problem with coefficient $\sigma(\mathbf{x})$ in the mass term, homogeneous Neumann BCs, space $S_2^0(\mathcal{M})$.

### Subpart strategy

| Part | Type | Strategy |
|------|------|----------|
| (a) | B | Fundamental lemma: strong form $\sigma(\mathbf{x})\dot{u} - \Delta u = 0$ in $\Omega$, $\nabla u \cdot \mathbf{n} = 0$ on $\partial\Omega$ |
| (b) | C | $\mathbf{M}_{ij} = \int_\Omega \sigma\, b_i^h b_j^h$, $\mathbf{A}_{ij} = \int_\Omega \nabla b_i^h \cdot \nabla b_j^h$; $\boldsymbol{\varphi} = \mathbf{0}$ |
| (c) | D | SDIRK-2 with $\zeta = 1-\sqrt{2}/2$: two stages with $(\mathbf{M}+\zeta\tau\mathbf{A})\boldsymbol{\kappa}_i = \text{RHS}_i$; multiply RK by $\mathbf{M}$ |
| (d) | F | Meta-Thm 9.2.8.5: $O(h^2 + \tau^2)$ in $H^1$; balance $\tau \sim h$; count refinements for target error reduction |

> [!tip] KEY INSIGHT
> Identical structure to HW 9-20. If you can do 9-20 on paper, you can do this exam problem.

> [!example] BOARD: SDIRK-2 stage 1 (homogeneous)
> $$(\mathbf{M} + \zeta\tau\mathbf{A})\boldsymbol{\kappa}_1 = -\tau\mathbf{A}\boldsymbol{\mu}^{(k)}$$

Code reference: [[LehrFEM-Solver-Convergence-Patterns#3. SDIRK-2 Timestepping]], NPDERepo `SDIRK/mastersolution`.

---

## 2024 Endterm 0-1 — Scalar parabolic evolution

**Folder (exam/HW PDF):** `ParabolicEvolutionAspects` | **HW:** **9-17** | **Sections:** §9.2.4, §9.2.7

> [!warning] Not `SobolevEvolutionProblem`
> That folder belongs to **Problem 9-12** (different Sobolev evolution model). 9-17 has **no** NPDERepo homework folder.

**Variational form (exam eq. 0.1.1):**
$$\int_{\partial\Omega} \frac{\partial u}{\partial t}\, v\,\mathrm{d}S + \int_\Omega \mathrm{grad}\, u \cdot \mathrm{grad}\, v\,\mathrm{d}\mathbf{x} = 0 \quad \forall v \in H^1(\Omega)$$

Space: $S_2^0(\mathcal{M})$ (quadratic).

### Subpart strategy

| Part | Type | Strategy |
|------|------|----------|
| (a) | C | $\mathbf{M}_{ij} = \int_{\partial\Omega} b_i^h b_j^h\,\mathrm{d}S$ (**boundary** assembly, codim 1); $\mathbf{A}_{ij} = \int_\Omega \nabla b_i^h \cdot \nabla b_j^h$ |
| (b) | B | Strong: $-\Delta u = 0$ in $\Omega$; on $\partial\Omega$: $\dot{u} + \nabla u \cdot \mathbf{n} = 0$ |
| (c) | D | Implicit Euler: $(\mathbf{M}+\tau\mathbf{A})\boldsymbol{\mu}^{(k+1)} = \mathbf{M}\boldsymbol{\mu}^{(k)}$ |
| (d) | theory | $\mathbf{M}$ only s.p.s.d. (interior DOFs decoupled from boundary mass); $\mathbf{A}$ kernel contains constants (Neumann-type) |

> [!warning] CAUTION
> **Most common mistake:** using $\mathbf{M}_{ij} = \int_\Omega b_i b_j$ instead of boundary integral.

---

## 2023 Endterm 0-3 — Two-step Radau RK for heat

**HW:** **9-14** | **Sections:** §9.2.4, §9.2.7

**Focus:** 2-stage Radau-3 Butcher tableau applied to $\mathbf{M}\dot{\boldsymbol{\mu}} = -\mathbf{A}\boldsymbol{\mu} + \boldsymbol{\varphi}$.

### Strategy

1. **(a) Type C:** Standard mass + stiffness; weighted $\rho(\mathbf{x})$ if given in variant.
2. **(b) Type D:** Write block system
   $$(\mathbf{I}_2 \otimes \mathbf{M} + \tau \mathcal{A} \otimes \mathbf{A}) \begin{pmatrix}\boldsymbol{\kappa}_1 \\ \boldsymbol{\kappa}_2\end{pmatrix} = \begin{pmatrix}\text{RHS}_1 \\ \text{RHS}_2\end{pmatrix}$$
   with Radau $\mathcal{A} = \begin{pmatrix}5/12 & -1/12 \\ 3/4 & 1/4\end{pmatrix}$.
3. Update: $\boldsymbol{\mu}^{(k+1)} = \boldsymbol{\mu}^{(k)} + \frac{3}{4}\boldsymbol{\kappa}_1 + \frac{1}{4}\boldsymbol{\kappa}_2$.

> [!tip] Contrast with SDIRK-2
> Radau is **not** SDIRK → cannot use two independent $N\times N$ solves with same matrix.

---

## 2022 Endterm 0-2 — RK single-step methods

**Sections:** §7.3.3, §9.2.7 (general RK theory)

**Focus:** Stability functions $R(z)$, order conditions, $A$- / $L(\pi)$-stability — not full MOL assembly.

### Strategy

- Apply RK to scalar model $\dot{y} = \lambda y$, $z = \tau\lambda$.
- Implicit Euler: $R(z) = 1/(1-z)$.
- Compare explicit vs implicit stability regions.
- Link to MOL: $z = \tau\lambda_i$ with $\lambda_i = O(h^{-2})$.

> [!note] Supplementary
> Primarily Ch.7; included because endterm Problem 0-2 slot often tests RK before parabolic-specific 0-3.

---

## 2022 Endterm 0-3 — Degenerate parabolic evolution

**Related HW:** **9-17** | **Sections:** §9.2.2, §9.2.3

**Focus:** Variational form where evolution appears only on part of the domain or boundary (degenerate mass operator).

### Strategy

1. Type B: identify where $\dot{u}$ appears (boundary vs volume).
2. Type C: $\mathbf{M}$ may be **singular** on interior DOFs — only boundary blocks nonzero.
3. Stability: energy norms with $\|\cdot\|_{\mathbf{M}}$ — may not be true norm on all of $\mathbb{R}^N$.
4. Implicit Euler still contractive in seminorm on range of $\mathbf{M}$.

---

## 2021 Endterm 0-3 — 2-stage implicit RK parabolic timestepping

**HW:** **9-1** (Radau-3 implementation) | **Sections:** §9.2.7

Same workflow as 2023 0-3: Kronecker system + update formula. Practice: [[Parabolic-Timestepping-Problems#Problem 9-1]].

---

## 2021 Endterm 0-1 — Embedded RK (supplementary)

**Chapter:** primarily §6.5.3 / §7.3.3 (embedded error estimation), not §9.2-specific.

**Endterm prep:** skim only — error control via embedded pairs; not recurring in 2022–2025 Ch.9 slots.

---

## Priority ranking for revision

| Rank | Problem | Why |
|------|---------|-----|
| 1 | 2025 0-2 | Latest + matches HW 9-20 |
| 2 | 2024 0-1 | Unusual $\mathbf{M}$ — tests understanding |
| 3 | 2023 0-3 | Kronecker pattern |
| 4 | 2022 0-3 | Degenerate operator |
| 5 | 2022 0-2 | RK stability background |

---

## Type mapping summary

| Exam problem | A | B | C | D | E | F | G |
|--------------|---|---|---|---|---|---|---|
| 2025 0-2 | | ✓ | ✓ | ✓ | | ✓ | |
| 2024 0-1 | | ✓ | ✓ | ✓ | | | |
| 2023 0-3 | | | ✓ | ✓ | | | |
| 2022 0-3 | | ✓ | ✓ | | | | |
| 2022 0-2 | | | | partial | | | |

Recipes: [[Endterm-Problem-Types-Recipes]].

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Ch9-Homework-Walkthrough]] | [[Parabolic-Timestepping-Problems]]
