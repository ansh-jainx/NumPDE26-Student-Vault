---
tags: [endterm, exam-critical, chapter-12, student]
---

# Endterm Ch.12 — Student Handout (Stokes FEM)

**Chapter 12** — saddle-point formulation, LBB, stable mixed elements

Related: [[Week-09-Stokes-I]], [[Week-10-Stokes-II]], [[Formulas-Stokes]], [[Stokes-Problems]]

---

## Strong form (no-slip)

$$-\mu\Delta\mathbf{v} + \nabla p = \mathbf{f}, \quad \mathrm{div}\,\mathbf{v} = 0 \text{ in } \Omega, \quad \mathbf{v} = \mathbf{0} \text{ on } \partial\Omega$$
$$\int_\Omega p\,\mathrm{d}\mathbf{x} = 0$$

---

## Saddle-point weak form (12.2.2.44)

Find $\mathbf{v} \in (H^1_0(\Omega))^d$, $p \in L^2(\Omega)$, $\lambda \in \mathbb{R}$:

| Form | Expression |
|------|------------|
| $a(\mathbf{v},\mathbf{w})$ | $\int_\Omega \mu\, D\mathbf{v} : D\mathbf{w}\,\mathrm{d}\mathbf{x}$ |
| $b(\mathbf{w},q)$ | $-\int_\Omega q\,\mathrm{div}\,\mathbf{w}\,\mathrm{d}\mathbf{x}$ |
| $\ell(\mathbf{w})$ | $\int_\Omega \mathbf{f}\cdot\mathbf{w}\,\mathrm{d}\mathbf{x}$ |

**Momentum:** $a(\mathbf{v},\mathbf{w}) + b(\mathbf{w},p) + \lambda\int_\Omega q = \ell(\mathbf{w})$ ∀$\mathbf{w}$.

**Incompressibility + pressure mean:** $b(\mathbf{v},q) + \lambda\int_\Omega p = 0$ ∀$q$.

> [!example] HOW TO: Derive from strong form
> 1. Test momentum with $\mathbf{w} \in (H^1_0)^d$.
> 2. IBP on $-\mu\Delta\mathbf{v}$ → $a(\mathbf{v},\mathbf{w})$.
> 3. IBP on $\nabla p$ → $b(\mathbf{w},p)$.
> 4. Test $\mathrm{div}\,\mathbf{v}=0$ with $q$.

---

## Block Galerkin system

$$\begin{pmatrix} \mathbf{A} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0} \end{pmatrix} \begin{pmatrix} \boldsymbol{\mu}_v \\ \boldsymbol{\mu}_p \end{pmatrix} = \begin{pmatrix} \boldsymbol{\varphi}_v \\ \mathbf{0} \end{pmatrix}$$

Pressure space often $L^2_*(\Omega) = \{q : \int_\Omega q = 0\}$.

---

## LBB (Thm 12.2.2.23)

- **LBB1:** coercivity of $a$ on $\ker B$.
- **LBB2 (inf-sup):** $\displaystyle\inf_q \sup_{\mathbf{v}} \frac{|b(\mathbf{v},q)|}{\|\mathbf{v}\|_{H^1}\|q\|_{L^2}} \geq \beta > 0$.

**Discrete version (12.3.3.25):** same with $U_h$, $Q_h$, discrete $b$ and $\|\mathbf{w}_h\|_a$.

---

## Why $P_1$–$P_1$ fails

Spurious pressure modes in $\ker B_h$ → checkerboard oscillations. Need **stable pair** satisfying discrete inf-sup.

---

## Stable element pairs

| Pair | $U_h$ | $Q_h$ | Typical rate ($H^1 \times L^2$) |
|------|-------|-------|----------------------------------|
| Taylor-Hood | $S_2^0$ (vector) | $S_1^0$ | $O(h^2)$ |
| MINI | $P_1$ + bubble | $P_1$ | $O(h^2)$ (velocity-led) |
| Crouzeix–Raviart | CR velocity | $P_0$ | $O(h)$ |
| **2025 Endterm** | $S_{2,0}^0$ | $S_0^{-1}$ (constants) | **$O(h)$ overall** |

> [!tip] 2025 Endterm 0-1(e)
> Velocity approx $O(h^2)$ but pressure on piecewise constants only $O(h)$ → sum dominated by pressure → **$O(h)$**.

---

## Dimension constraint (2025 0-1.b)

$$\dim U_h \geq \dim Q_h$$

Necessary for unique discrete pressure — **not** sufficient for stability.

---

## Refinement monotonicity (2025 0-1.d)

Given stable $(U_h, Q_h)$ and finer spaces $\tilde{U}_h \supset U_h$, $\tilde{Q}_h \supset Q_h$:

| Pair | Guaranteed stable? |
|------|-------------------|
| $(U_h, \tilde{Q}_h)$ — enlarge pressure only | **YES** |
| $(\tilde{U}_h, Q_h)$ — enlarge velocity only | **YES** |
| $(\tilde{U}_h, \tilde{Q}_h)$ — enlarge both | **NO** |

> [!warning] Exam note
> Official solution **table** (use this on the exam). The prose sentence claiming only $(U_h, \tilde{Q}_h)$ is stable contradicts the marked table — follow the checkmarks.

---

## Convergence (Thm 12.3.3.13)

For stable pair:
$$\|\mathbf{v}-\mathbf{v}_h\|_{H^1} + \|p-p_h\|_{L^2} \leq C\left(\inf_{\mathbf{w}_h\in U_h}\|\mathbf{v}-\mathbf{w}_h\|_{H^1} + \inf_{q_h\in Q_h}\|p-q_h\|_{L^2}\right)$$

---

## Exam focus

**Only Ch.12 endterm in 2021–2025 corpus:** **2025 Endterm 0-1** (40 pts, theory).

Drill: [[Endterm-Ch12-Exam-Compendium]] | HW **12-4**.

---

## Practice exercises

1. **(10 pts)** Fill in saddle-point form for given Stokes strong form (2025 0-1.a style).
2. **(5 pts)** $\dim U_h$ vs $\dim Q_h$ — choose inequality.
3. **(10 pts)** Write discrete inf-sup with correct $b$ and norms.
4. **(5 pts)** YES/NO: which refined spaces stay stable?
5. **(10 pts)** Convergence rate for $S_{2,0}^0 \times S_0^{-1}$ on uniform refinement.
6. **(8 pts)** Block matrix: what goes in $\mathbf{A}$, $\mathbf{B}$?
7. **(6 pts)** Why is pressure defined up to constant without pinning?
8. **(6 pts)** Name two stable pairs and their orders.

---

## Self-check

1. Write $a(\mathbf{v},\mathbf{w})$ and $b(\mathbf{w},q)$.
2. Block system size: $n_u + n_p$ equations?
3. LBB2 in one sentence.
4. Taylor-Hood local DOFs on triangle (2D)?
5. $P_1$–$P_1$ failure mechanism?
6. 2025 exam convergence rate?
7. $(\tilde{U}_h, \tilde{Q}_h)$ — guaranteed stable?
8. $\int_\Omega p = 0$ purpose?
9. Thm 12.3.3.13 vs Céa's lemma?
10. CR: conforming velocity?

**Answers:** [[Endterm-Practice-Set#Ch.12 self-check answers]]

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Problem-Types-Recipes]] | [[LehrFEM-Stokes-Patterns]]
