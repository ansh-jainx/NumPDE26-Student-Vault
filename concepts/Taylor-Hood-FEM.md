---
tags: [chapter-12, Stokes, Taylor-Hood, mixed-FEM, exam-critical]
first_appears: "[[Week-10-Stokes-II]]"
---

# Taylor-Hood FEM

**Reference:** §12.3.4

---

## Element pair

On triangular mesh $\mathcal{M}$:

| Field | Space | DOFs per triangle |
|-------|-------|-------------------|
| Velocity $\mathbf{u}_h$ | $(S_2^0(\mathcal{M}))^d$ | 6 per component |
| Pressure $p_h$ | $S_1^0(\mathcal{M})$ | 3 |

**Taylor-Hood:** $P_2$–$P_1$ (quadratic velocity, linear pressure).

## Why stable

Satisfies **discrete LBB** — inherits continuous inf-sup from [[LBB-Condition]]. Optimal convergence: $\|\mathbf{u} - \mathbf{u}_h\|_{H^1} = O(h^2)$, $\|p - p_h\|_{L^2} = O(h^2)$ for smooth solutions.

## Block system

$$\begin{pmatrix} \mathbf{A} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0} \end{pmatrix} \begin{pmatrix} \boldsymbol{\mu}_u \\ \boldsymbol{\mu}_p \end{pmatrix} = \begin{pmatrix} \boldsymbol{\varphi}_u \\ \mathbf{0} \end{pmatrix}$$

- $\mathbf{A}$: viscous stiffness (strain energy)
- $\mathbf{B}$: discrete divergence operator

> [!tip] Exam
> **2025 Endterm 0-1** — FEM for Stokes BVPs. Know Taylor-Hood spaces and block structure.

---

**Problems:** 12-1, 12-3 | **Related:** [[LehrFEM-Stokes-Patterns]], [[Pressure-Instability]], [[Crouzeix-Raviart-FEM]]
