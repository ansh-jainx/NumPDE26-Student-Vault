---
tags: [chapter-2, parametric, isoparametric, curved-elements]
first_appears: "[[Week-05-Parametric-FEM-and-Error]]"
---

# Parametric FEM

**Reference:** §2.8

---

## Idea

For domains with **curved boundaries**, straight-edged triangles introduce geometry error. Parametric FEM uses polynomial maps $\Phi_K: \hat{K} \to K$ that can curve the edges.

## Affine Equivalence

For straight-edged elements: $\Phi_K$ is affine (linear map + translation). All element computations reduce to the reference element $\hat{K}$:

$$\mathbf{A}_K = |\det \mathbf{F}_K|\,\mathbf{F}_K^{-1}\,\hat{\mathbf{A}}\,\mathbf{F}_K^{-T}$$

where $\hat{\mathbf{A}}$ is the stiffness matrix on $\hat{K}$ (computed once).

## Isoparametric Elements

Use the **same** polynomial basis for both:
1. Geometry: $\Phi_K(\hat{\mathbf{x}}) = \sum_i \mathbf{a}_i\,\hat{b}_i(\hat{\mathbf{x}})$
2. Solution: $u_h|_K = \sum_i \mu_i\,\hat{b}_i \circ \Phi_K^{-1}$

> [!warning] Variational crime
> Curved elements mean $\Phi_K$ is no longer affine → [[Local-Computations|gradient transformation]] involves a non-constant Jacobian → quadrature introduces additional error. This is a "variational crime" (§3.5) — the discrete bilinear form $a_h \neq a$.

---

**Problems:** 2-13 | **Related:** [[Local-Computations]], [[Lagrangian-FEM]], [[Variational-Crimes]]
