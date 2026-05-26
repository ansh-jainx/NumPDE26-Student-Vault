---
tags: [exam, exam-critical, chapter-1, deep-dive]
---

# Exam Deep Dive — Elliptic Weak Form

**Theme:** Midterm **0-1** elliptic chain (7 appearances 2021–2026) | **Types A/B** | **HW:** 1-9, 1-10, 1-11

> Master bank: [[Exam-Master-Bank#Ch1]] | Recipes: [[Exam-Problem-Types-Full-Course#Type A — Elliptic weak form]]

---

## Anchor exams

| Year | Exam | Problem | Title | HW |
|------|------|---------|-------|-----|
| 2026 | Midterm | 0-1 | Reformulating elliptic variational problem | 1-10, 1-11 |
| 2023 | Midterm | 0-1 | BVP → variational problems | 1-10 |
| 2022 | Midterm | 0-1 | BVP, variational, quadratic minimization | 1-1, 1-10 |
| 2021 | Midterm | 0-1 | Elliptic BVP from weak formulations | 1-9 |

PDFs: `NPDE26_Midterm_sols.pdf`, `NPDE23_Midterm_sols.pdf`, `NPDE22_Midterm_sols.pdf`, `NPDE21_Midterm_sols.pdf`.

---

## Universal strategy (Type A)

> [!example] HOW TO: Midterm 0-1
> 1. Write strong form: $-\nabla\cdot(\alpha\nabla u) + \beta u = f$ in $\Omega$.
> 2. Multiply by test $v$; integrate over $\Omega$.
> 3. IBP (Green Thm **1.5.2.7**): $\int_\Omega \alpha\nabla u\cdot\nabla v - \int_{\partial\Omega} \alpha\,\frac{\partial u}{\partial n}\,v$.
> 4. Replace $\partial u/\partial n$ using BC data → essential vs natural.
> 5. State trial space ($H^1_0$ for homogeneous Dirichlet, etc.).

> [!example] HOW TO: Type B (reverse)
> 1. Assume smooth $u$; IBP weak form terms back to strong.
> 2. Fundamental lemma (**1.5.3.4**) on interior → PDE.
> 3. Boundary integrals → Neumann/Robin data.

---

## 2026 Midterm 0-1

**Focus:** Mixed essential/natural BCs on different parts of $\partial\Omega$.

**Pitfall:** Forgetting to restrict test space on Dirichlet portions while retaining natural boundary integrals elsewhere.

**HW drill:** [[Elliptic-BVP-Theory-Problems#Problem 1-10]], 1-11 (mixed BC).

---

## 2023 / 2022 / 2021 Midterm 0-1

Progression:
- **2021:** Pure weak ↔ strong translation.
- **2022:** Adds **quadratic minimization** equivalence (Thm **1.4.2.7**).
- **2023:** Multi-part BVP with several boundary conditions.

---

## NPDERepo notes

| Folder | HW | Role |
|--------|-----|------|
| `VPtoBVP` | 1-10 | Coding: VP reformulation |

Exam folder appears on some finals/midterm variants — see [[Exam-Folder-Crosswalk]].

---

## Links

- Week: [[Week-01-Elliptic-BVPs-I]], [[Week-02-Elliptic-BVPs-II]]
- Concepts: [[Lax-Milgram-Theorem]], [[Essential-vs-Natural-BCs]], [[Linear-Variational-Problem]]
- Problems: [[Elliptic-BVP-Theory-Problems]]
