---
tags: [chapter-10, SUPG, streamline-diffusion, stabilization, exam-critical]
first_appears: "[[Week-08-Convection-Diffusion]]"
---

# Streamline Diffusion (SUPG)

**Reference:** §10.2.2.2

---

## Idea

Add a **consistency-preserving** stabilization term along streamlines. For the convection-diffusion operator $-\varepsilon\Delta u + \mathbf{v}\cdot\nabla u$, the SUPG modification adds:

$$\tau_K \int_K (\mathbf{v} \cdot \nabla u)\,(\mathbf{v} \cdot \nabla w)\,\mathrm{d}\mathbf{x}$$

to the bilinear form, where $\tau_K > 0$ is a cell-wise stabilization parameter (often $\tau_K \sim h_K / \|\mathbf{v}\|_K$).

## Compared to upwind

| Method                | Mechanism             | Accuracy                                      |
| --------------------- | --------------------- | --------------------------------------------- |
| [[Upwind-Quadrature]] | Quadrature point bias | 1st order in layer regions                    |
| SUPG                  | Extra bilinear term   | Can retain $O(h^2)$ in $L^2$ away from layers |

> [!theorem] Key observation (Exp. 10.2.2.37–38)
> SUPG eliminates spurious oscillations for $\varepsilon \to 0$ while preserving optimal $L^2$ convergence rates in $h$-refinement (when layers are resolved).

## Parameter choice

$\tau_K$ must balance stability and accuracy. Too large $\Rightarrow$ excessive numerical diffusion; too small $\Rightarrow$ instability returns.

---

**Problems:** 10-6, 10-7 | **Related:** [[Upwind-Quadrature]], [[Singular-Perturbation]], [[Variational-Crimes]]
