---
tags: [endterm, exam-critical, practice]
---

# Endterm Practice Set (Ch.9 & Ch.12)

Mixed mock questions tagged by exam origin. Work under timed conditions (90 min for full set ≈ half exam load).

---

## Section A — Parabolic / MOL (Ch.9)

### A1 (2024 Endterm 0-1 style, 12 pts)

On $\Omega \subset \mathbb{R}^2$, find $u:]0,T[ \to H^1(\Omega)$ such that
$$\int_{\partial\Omega} \frac{\partial u}{\partial t}\, v\,\mathrm{d}S + \int_\Omega \nabla u \cdot \nabla v\,\mathrm{d}\mathbf{x} = 0 \quad \forall v \in H^1(\Omega).$$

(a) Give $(\mathbf{M})_{ij}$ and $(\mathbf{A})_{ij}$ for $S_2^0(\mathcal{M})$. (4 pts)

(b) Recover strong PDE + BCs. (4 pts)

(c) Implicit Euler fully discrete scheme. (4 pts)

<details>
<summary>Solution sketch</summary>

(a) $\mathbf{M}_{ij} = \int_{\partial\Omega} b_i^h b_j^h\,\mathrm{d}S$, $\mathbf{A}_{ij} = \int_\Omega \nabla b_i^h \cdot \nabla b_j^h$.

(b) $-\Delta u = 0$ in $\Omega$; $\dot{u} + \nabla u \cdot \mathbf{n} = 0$ on $\partial\Omega$.

(c) $(\mathbf{M}+\tau\mathbf{A})\boldsymbol{\mu}^{(k+1)} = \mathbf{M}\boldsymbol{\mu}^{(k)}$.

</details>

---

### A2 (2025 Endterm 0-2 style, 15 pts)

Variational form: $\int_\Omega \sigma(\mathbf{x})\,\dot{u}\, v + \int_\Omega \nabla u \cdot \nabla v = 0$, Neumann BCs, $S_2^0(\mathcal{M})$.

(a) Strong form. (3 pts)

(b) MOL ODE. (4 pts)

(c) SDIRK-2 stage equations ($\zeta = 1-\sqrt{2}/2$). (5 pts)

(d) Balanced refinement for $H^1$ error — relation between $h$ and $\tau$. (3 pts)

<details>
<summary>Solution sketch</summary>

(a) $\sigma\dot{u} - \Delta u = 0$, $\nabla u \cdot \mathbf{n} = 0$.

(b) $\mathbf{M}_{ij} = \int \sigma b_i b_j$, $\mathbf{A}_{ij} = \int \nabla b_i \cdot \nabla b_j$.

(c) $(\mathbf{M}+\zeta\tau\mathbf{A})\boldsymbol{\kappa}_i = \text{stage RHS}$; two stages, same matrix.

(d) Meta-thm: $O(h^2+\tau^2)$ → $\tau \sim h$.

</details>

---

### A3 (2023 Endterm 0-3 style, 10 pts)

Given $\mathbf{M}\dot{\boldsymbol{\mu}} = -\mathbf{A}\boldsymbol{\mu}$, write the $2N \times 2N$ block system for 2-stage Radau-3 with Butcher matrix $\mathcal{A} = \begin{pmatrix}5/12 & -1/12\\ 3/4 & 1/4\end{pmatrix}$.

<details>
<summary>Solution sketch</summary>

$(\mathbf{I}_2 \otimes \mathbf{M} + \tau\mathcal{A} \otimes \mathbf{A}) \boldsymbol{\kappa} = \text{RHS}$ with $\boldsymbol{\kappa} = (\boldsymbol{\kappa}_1^T, \boldsymbol{\kappa}_2^T)^T$.

</details>

---

## Section B — Stokes (Ch.12)

### B1 (2025 Endterm 0-1 style, 25 pts)

(a) Complete saddle-point form (12.2.2.44) for no-slip Stokes. (10 pts)

(b) $\dim U_h$ vs $\dim Q_h$? (5 pts)

(c) Discrete inf-sup inequality. (10 pts)

<details>
<summary>Solution sketch</summary>

See [[Endterm-Ch12-Exam-Compendium#2025 Endterm 0-1]].

(b) $\geq$.

(c) $\sup_{w_h\in U_h} \frac{|\int q_h \mathrm{div}\, w_h|}{\|w_h\|_a} \geq \beta \|q_h\|_{L^2}$.

</details>

---

### B2 (2025 Endterm 0-1.e style, 10 pts)

Stable pair $S_{2,0}^0(\mathcal{M}) \times S_0^{-1}(\mathcal{M})$, smooth exact solution. Sharp rate for $\|\mathbf{v}-\mathbf{v}_h\|_{H^1} + \|p-p_h\|_{L^2}$?

<details>
<summary>Solution sketch</summary>

$O(h)$ — pressure best approximation on constants is first order (Thm 12.3.3.13).

</details>

---

### B3 (Concept, 8 pts)

Explain in 4 sentences why equal-order $P_1$–$P_1$ Stokes fails.

<details>
<summary>Solution sketch</summary>

Discrete divergence operator has nontrivial kernel paired with spurious pressure modes; discrete inf-sup fails; checkerboard pressures satisfy $\mathrm{div}\,\mathbf{u}_h \approx 0$ without physical meaning; need Taylor-Hood/MINI/CR or stabilization.

</details>

---

## Section C — Mixed quick (20 min)

1. Robin BC: which matrix gets edge integral?
2. SDIRK-2: how many factorizations per step?
3. Write LBB2 in words.
4. Block system dimensions if $n_u$ velocity DOFs, $n_p$ pressure DOFs?
5. Explicit Euler CFL for MOL?

<details>
<summary>Answers</summary>

1. $\mathbf{A}$ (stiffness)
2. One
3. Pressure gradient controlled by velocity test functions uniformly
4. $(n_u+n_p) \times (n_u+n_p)$ with zero pressure block
5. $\tau = O(h^2)$

</details>

---

## Ch.9 self-check answers

1. $\mathbf{M}\dot{\boldsymbol{\mu}} + \mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$
2. $\mathbf{A}$
3. $\zeta = 1 - \sqrt{2}/2$
4. Two solves, one factorization
5. $-\Delta u = 0$; boundary $\dot{u} + \nabla u \cdot \mathbf{n} = 0$
6. $C(h^2 + \tau^2)$; balance $\tau \sim h$
7. $\lambda_{\max} = O(h^{-2})$
8. $2N \times 2N$
9. No (natural Neumann)
10. Mass bilinear form $m(u,v) = \int \sigma u v$

---

## Ch.12 self-check answers

1. $a = \int \mu Dv:Dw$; $b = -\int q\,\mathrm{div}\, w$
2. Yes, $n_u + n_p$ unknowns
3. Pressure modes must be detectable by divergence pairing with velocity tests
4. 6 scalar $P_2$ + 3 pressure per triangle (2D vector: 12 velocity + 3 pressure local DOFs before global assembly)
5. Spurious kernel of $B_h$
6. $O(h)$ for $S_{2,0}^0 \times S_0^{-1}$
7. No — $(\tilde{U}_h, \tilde{Q}_h)$ is **not** guaranteed stable
8. Remove pressure null space / uniqueness
9. Mixed Céa bounds velocity + pressure errors via inf-sup
10. Non-conforming

---

**Navigation:** [[Endterm-Prep-Ch9-Ch12]] | [[Endterm-Ch9-Student-Handout]] | [[Endterm-Ch12-Student-Handout]]
