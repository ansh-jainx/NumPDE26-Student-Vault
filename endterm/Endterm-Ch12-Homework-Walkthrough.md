---
tags: [endterm, exam-critical, chapter-12, homework]
---

# Endterm Ch.12 — Homework Walkthrough

Priority homework for endterm prep from `NPDEFL_Problems.pdf` and [[Stokes-Problems]].

---

## Priority tier 1 — endterm theory

### Problem 12-4 — FEM for Stokes BVPs (theory)

**Exam mirror:** **2025 Endterm 0-1** (direct template)

| Task | Endterm link |
|------|--------------|
| Write $a$, $b$, block system | 0-1(a) |
| Pressure pinning / $L^2_*$ | 0-1(a) multiplier $\lambda$ |
| Discrete LBB statement | 0-1(c) |
| Stable pair definition | 0-1 assumption |

> [!example] HOW TO: Block system on paper
> 1. Choose $U_h \subset (H^1_0)^d$, $Q_h \subset L^2_*$.
> 2. $(\mathbf{A})_{ij} = a(\mathbf{v}_j, \mathbf{v}_i)$, $(\mathbf{B})_{kj} = b(\mathbf{v}_j, q_k)$.
> 3. Solve $(\mathbf{A}, \mathbf{B}^T; \mathbf{B}, \mathbf{0})(\boldsymbol{\mu}_v; \boldsymbol{\mu}_p) = (\boldsymbol{\varphi}; \mathbf{0})$.

**Code folder:** — (theory only)

---

## Priority tier 2 — solidify stable pairs

### Problem 12-3 — Taylor-Hood BVP (`TaylorHoodNonMonolithic`)

- Manufactured solution → $O(h^2)$ for $\mathbf{v}$ and $p$ in smooth case.
- **Contrast** with exam pair $S_{2,0}^0 \times S_0^{-1}$ where rate is only $O(h)$ overall.

### Problem 12-1 — Pipe flow (`StokesPipeFlow`)

- Full Taylor-Hood implementation.
- Summer final coding — not 2025 endterm.
- Patterns: [[LehrFEM-Stokes-Patterns]]

---

## Priority tier 3 — alternative stable elements

| Problem | Element | When to study |
|---------|---------|---------------|
| **12-2** MINI | $P_1$+bubble / $P_1$ | 2024 Winter final |
| **12-5** Stab $P_1$–$P_1$ | equal-order + penalty | 2025 Summer final |

Know **names and why naive $P_1$–$P_1$ fails** — endterm may ask conceptually even if coding is out of scope.

---

## Endterm vs homework focus

| Skill | 12-4 / endterm | 12-1 / 12-3 |
|-------|----------------|-------------|
| Saddle-point weak form | **required** | practice |
| Discrete inf-sup | **required** | implicit |
| Block matrix structure | **required** | assembly |
| LehrFEM code | not on 2025 endterm | required for finals |
| Convergence rate analysis | **2025 0-1(e)** | 12-3 numerical |

---

## Suggested study order

1. **12-4** on paper (2 h) — all theory boxes
2. **2025 Endterm 0-1** timed (90 min) — [[Endterm-Ch12-Exam-Compendium]]
3. **12-3** convergence numerically (optional, 3 h)
4. **12-1** code only if targeting summer final (6+ h)

---

## Cross-chapter connections

- **2-22** — saddle-point preview
- **2-14**, **3-16** — CR non-conforming (Stokes CR element §12.3.5)
- **Week 13** — discrete LBB reappears in magnetostatics

---

**Navigation:** [[Endterm-Ch12-Exam-Compendium]] | [[Stokes-Problems]] | [[Week-10-Stokes-II]]
