---
tags: [endterm, exam-critical, chapter-12, exam-bank]
---

# Endterm Ch.12 — Exam Compendium

**Only endterm Ch.12 problem in corpus 2021–2025:** **2025 Endterm 0-1** (40 pts, theory-only).

Source: `NPDE25_Endterm_sols.pdf` | Repo folder: `StokesVPFEM` | HW: **12-4**, **12-3**, **12-1**

---

## 2025 Endterm 0-1 — FEM for Stokes BVPs

**Builds on:** §12.2.2, §12.3.2, §12.3.3 | **No implementation**

### Problem setup

Stokes on $\Omega \subset \mathbb{R}^2$ with $\mu > 0$, $\mathbf{f} \in L^2(\Omega)$:
$$-\mu\Delta\mathbf{v} + \nabla p = \mathbf{f}, \quad \mathrm{div}\,\mathbf{v} = 0, \quad \int_\Omega p = 0, \quad \mathbf{v} = \mathbf{0} \text{ on } \partial\Omega$$

Assume stable pair $(U_h, Q_h)$ with $Q_h \subset L^2_*(\Omega)$.

---

### (0-1.a) — 10 pts — Fill-in variational form

**Type A** — recall (12.2.2.44).

> [!example] Solution structure
> $$a(\mathbf{v},\mathbf{w}) = \int_\Omega \mu D\mathbf{v}:D\mathbf{w}\,\mathrm{d}\mathbf{x} = \int_\Omega \mathbf{f}\cdot\mathbf{w}\,\mathrm{d}\mathbf{x}$$
> $$-\int_\Omega p\,\mathrm{div}\,\mathbf{w}\,\mathrm{d}\mathbf{x} + \lambda\int_\Omega q\,\mathrm{d}\mathbf{x} = 0 \quad \text{(momentum for all } \mathbf{w}\text{)}$$
> $$-\int_\Omega q\,\mathrm{div}\,\mathbf{v}\,\mathrm{d}\mathbf{x} + \lambda\int_\Omega p\,\mathrm{d}\mathbf{x} = 0 \quad \text{(for all } q\text{)}$$

**Exam boxes:** third box first line = **0** (nothing); second box second line = **0**.

**Strategy:** Do not derive under time pressure — memorize template and adapt signs.

---

### (0-1.b) — 5 pts — Dimension relation

**Answer:** $\dim U_h \geq \dim Q_h$

**Why:** Necessary for uniqueness of discrete pressure (§12.3.1). Stability of pair does **not** imply strict inequality.

> [!warning] CAUTION
> Students pick "$=$" or "$>$" — wrong without extra hypotheses.

---

### (0-1.c) — 10 pts — Discrete inf-sup (Thm 12.3.2.15)

Complete (12.3.3.25):

$$\sup_{\mathbf{w}_h \in U_h} \frac{\left|\int_\Omega q_h\,\mathrm{div}\,\mathbf{w}_h\,\mathrm{d}\mathbf{x}\right|}{\|\mathbf{w}_h\|_a} \geq \beta \|q_h\|_{L^2(\Omega)} \quad \forall q_h \in Q_h$$

with $\|\mathbf{w}_h\|_a^2 = \int_\Omega \mu D\mathbf{w}_h : D\mathbf{w}_h\,\mathrm{d}\mathbf{x}$.

**Acceptable variants (per official solution):** denominator may use $| \mathbf{w}_h|_{H^1}$ or $\|\mathbf{w}_h\|_{H^1}$ via Poincaré–Friedrichs.

---

### (0-1.d) — 5 pts — Refinement stability table

Given stable $(U_h, Q_h)$ and finer spaces $\tilde{U}_h \supset U_h$, $\tilde{Q}_h \supset Q_h$:

| Pair | Guaranteed stable? |
|------|---------------------|
| $(U_h, \tilde{Q}_h)$ | **YES** ✓ |
| $(\tilde{U}_h, Q_h)$ | **YES** ✓ |
| $(\tilde{U}_h, \tilde{Q}_h)$ | **NO** ✗ |

**Reasoning:**
- $(\tilde{U}_h, Q_h)$: larger velocity space → sup in inf-sup only increases → **YES**.
- $(U_h, \tilde{Q}_h)$: official table marks **YES** (finer pressure on same velocity space).
- $(\tilde{U}_h, \tilde{Q}_h)$: both enlarged → **a priori undetermined** → **NO**.

> [!warning] PDF inconsistency
> The official solution prose says “only $(U_h, \tilde{Q}_h)$ is predictably stable,” but the **marked answer table** gives YES for both $(U_h, \tilde{Q}_h)$ and $(\tilde{U}_h, Q_h)$. Use the table on the exam.

---

### (0-1.e) — 10 pts — Convergence rate

**Spaces:** $U_h = S_{2,0}^0(\mathcal{M})$ (quadratic vector FE), $Q_h = S_0^{-1}(\mathcal{M})$ (piecewise constants). Stable pair (Exp. 12.3.2.1).

**Answer:**
$$\|\mathbf{v} - \mathbf{v}_h\|_{H^1(\Omega)} + \|p - p_h\|_{L^2(\Omega)} = O(h_{\mathcal{M}}) \quad \text{as } h_{\mathcal{M}} \to 0$$

**Proof sketch (exam level):**
1. Invoke saddle-point Céa **Thm 12.3.3.13**.
2. Best velocity approximation: $O(h^2)$ from Cor. 3.3.3.4 on $S_{2,0}^0$.
3. Best pressure approximation on $S_0^{-1}$: $O(h)$ via local $L^2$ projection + Poincaré–Friedrichs on each cell (Thm 1.8.0.20).
4. Pressure error **dominates** → overall first order.

> [!tip] Contrast Taylor-Hood
> $S_2^0 \times S_1^0$ gives $O(h^2)$ for both — exam deliberately uses **constant pressure** to test best-approximation bottleneck.

---

## Stokes patterns on other exams (supplementary)

Not in Endterm 2021–2025 Ch.12 slot, but useful for coding finals:

| Exam | Problem | Topic | HW |
|------|---------|-------|-----|
| 2024 Summer | 1-3 | Taylor-Hood implementation | 12-1, 12-3 |
| 2024 Winter | 1-3 | MINI element | 12-2 |
| 2025 Summer | 1-2 | Stabilized $P_1$–$P_1$ | 12-5 |

See [[Endterm-Code-Cheatsheet#Summer final appendix]].

---

## Type mapping — 2025 0-1

| Part | A | B | C | D | E | F |
|------|---|---|---|---|---|---|
| (a) | ✓ | | | | | |
| (b) | | | | | | theory |
| (c) | | | | | | theory |
| (d) | | | | | | theory |
| (e) | | | | | | ✓ |

---

## Revision checklist for 2025 0-1

- [ ] Recite (12.2.2.44) from memory
- [ ] Write discrete inf-sup with correct $b$
- [ ] Explain $\dim U_h \geq \dim Q_h$
- [ ] Answer refinement YES/NO table
- [ ] Derive $O(h)$ rate for $S_{2,0}^0 \times S_0^{-1}$

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Ch12-Homework-Walkthrough]] | [[Stokes-Problems]] | [[LBB-Condition]]
