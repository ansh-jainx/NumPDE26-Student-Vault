---
tags: [chapter-12, Stokes, saddle-point, mixed, exam-critical]
first_appears: "[[Week-09-Stokes-I]]"
---

# Stokes Saddle-Point Formulation

**Reference:** §12.2.2–§12.2.3

---

## Mixed variational form (12.2.2.19)

Find $(\mathbf{u}, p) \in (H_0^1(\Omega))^d \times L^2(\Omega)$:

$$\begin{aligned}
a(\mathbf{u}, \mathbf{w}) + b(\mathbf{w}, p) &= \ell(\mathbf{w}) && \forall \mathbf{w} \in (H_0^1)^d, \\
b(\mathbf{u}, q) &= 0 && \forall q \in L^2(\Omega),
\end{aligned}$$

| Form | Definition |
|------|------------|
| $a(\mathbf{u}, \mathbf{w})$ | $\int_\Omega \mu\, D\mathbf{u} : D\mathbf{w}\,\mathrm{d}\mathbf{x}$ |
| $b(\mathbf{w}, q)$ | $-\int_\Omega q\,\mathrm{div}\,\mathbf{w}\,\mathrm{d}\mathbf{x}$ |
| $\ell(\mathbf{w})$ | $\int_\Omega \mathbf{f} \cdot \mathbf{w}\,\mathrm{d}\mathbf{x}$ |

> [!info] Sign convention
> Some texts use $b(\mathbf{u},q) = \int q\,\mathrm{div}\,\mathbf{u}$. Be consistent with the script's (12.2.2.19).

## Strong form recovery

Integration by parts on the constraint equation gives $\mathrm{div}\,\mathbf{u} = 0$. The momentum equation gives $-\mu\Delta\mathbf{u} + \nabla p = \mathbf{f}$.

## Abstract template (12.2.2.11)

Special case of constrained quadratic minimization: find $(v^*, p^*) \in U \times Q$ with $a$ s.p.d. on $U$ and constraint $Bv = 0$.

---

**Problems:** 12-4 | **Related:** [[LBB-Condition]], [[Stokes-Constrained-Variational]], [[Formulas-Stokes]]
