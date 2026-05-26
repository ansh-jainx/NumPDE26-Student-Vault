---
tags: [chapter-9, stiffness, stability, eigenvalue, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Stiffness of Parabolic MOL ODEs

**Reference:** §9.2.7.15–9.2.7.26

---

## The Problem

The generalized eigenvalue problem $\mathbf{A}\boldsymbol{\psi}_i = \lambda_i\mathbf{M}\boldsymbol{\psi}_i$ decouples the [[Method-of-Lines]] ODE into $N$ scalar ODEs $\dot{\eta}_i + \lambda_i\eta_i = \ldots$

For FEM discretization of the Laplacian: $\lambda_{\max} = O(h^{-2})$.

Explicit Euler needs $|1 - \tau\lambda_i| < 1$ for all $i$, so:

$$\tau < \frac{2}{\lambda_{\max}} = O(h^2) \quad \text{(stability kills efficiency)}$$

> [!warning] Stiff IVP (Notion 7.2.0.7)
> Stability imposes much tighter timestep constraints on explicit methods than accuracy requires.

## Consequence

Use **$L(\pi)$-stable implicit methods**: implicit Euler, SDIRK-2, Radau collocation. These damp all eigencomponents without timestep restriction.

---

**Problems:** 9-3 (analysis), Exp. 9.2.7.10/13 (numerical evidence) | **Related:** [[Timestepping-MOL]]
