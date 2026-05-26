---
tags: [formulas, chapter-12, Stokes]
---

# Stokes — Quick Reference

---

## Strong form

$$-\mu\,\Delta \mathbf{u} + \nabla p = \mathbf{f} \quad \text{in } \Omega, \qquad \mathrm{div}\,\mathbf{u} = 0 \quad \text{in } \Omega, \qquad \mathbf{u} = \mathbf{0} \text{ on } \partial\Omega$$

## Saddle-point variational form (12.2.2.19)

$$\int_\Omega \mu\, D\mathbf{u} : D\mathbf{w} - \int_\Omega p\,\mathrm{div}\,\mathbf{w} = \int_\Omega \mathbf{f}\cdot\mathbf{w} \quad \forall \mathbf{w} \in (H_0^1)^d$$
$$\int_\Omega q\,\mathrm{div}\,\mathbf{u} = 0 \quad \forall q \in L^2(\Omega)$$

## LBB (Thm 12.2.2.23)

- **LBB1:** $a(\mathbf{v},\mathbf{v}) \geq \alpha \|\mathbf{v}\|_{H^1}^2$
- **LBB2:** $\displaystyle \inf_{q \in L^2} \sup_{\mathbf{v} \in H_0^1} \frac{-\int q\,\mathrm{div}\,\mathbf{v}}{\|\mathbf{v}\|_{H^1}\|q\|_{L^2}} \geq \beta > 0$

## Discrete block system

$$\begin{pmatrix} \mathbf{A} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0} \end{pmatrix} \begin{pmatrix} \boldsymbol{\mu}_u \\ \boldsymbol{\mu}_p \end{pmatrix} = \begin{pmatrix} \boldsymbol{\varphi}_u \\ \mathbf{0} \end{pmatrix}$$

## Taylor-Hood spaces

$$\mathbf{u}_h \in (S_2^0(\mathcal{M}))^d, \qquad p_h \in S_1^0(\mathcal{M})$$

---

**Related:** [[Stokes-Saddle-Point]], [[LBB-Condition]], [[Taylor-Hood-FEM]], [[Week-09-Stokes-I]], [[Week-10-Stokes-II]]
