---
tags: [chapter-2, reference-element, quadrature, gradient-transformation]
first_appears: "[[Week-04-FEM-II]]"
---

# Local Computations

**Reference:** §2.7.5

---

## Reference Element

All computations are done on a **reference element** $\hat{K}$:
- Reference triangle: $\hat{K} = \{(\hat{x}_1, \hat{x}_2) : \hat{x}_1, \hat{x}_2 \geq 0,\; \hat{x}_1 + \hat{x}_2 \leq 1\}$
- Affine map (Lemma 2.7.5.14): $\Phi_K: \hat{K} \to K$, $\mathbf{x} = \Phi_K(\hat{\mathbf{x}}) = \mathbf{F}_K\,\hat{\mathbf{x}} + \boldsymbol{\tau}_K$

## Gradient Transformation (Lemma 2.8.3.10, §2.8.3)

$$(\nabla_{\hat{\mathbf{x}}}\,\hat{u})(\hat{\mathbf{x}}) = \mathbf{F}_K^T\,(\nabla_{\mathbf{x}} u)(\Phi_K(\hat{\mathbf{x}}))$$

Equivalently: $\nabla_{\mathbf{x}} u = \mathbf{F}_K^{-T}\,\nabla_{\hat{\mathbf{x}}}\,\hat{u}$, where $\mathbf{F}_K = D\Phi_K$ is the Jacobian of the affine map.

## Integral Transformation

$$\int_K g(\mathbf{x})\,\mathrm{d}\mathbf{x} = |\det \mathbf{F}_K|\,\int_{\hat{K}} g(\Phi_K(\hat{\mathbf{x}}))\,\mathrm{d}\hat{\mathbf{x}}$$

Note: $|\det \mathbf{F}_K| = 2\,|K|$ for triangles.

## Quadrature

Approximate integrals on $\hat{K}$ using quadrature rules:

$$\int_{\hat{K}} f\,\mathrm{d}\hat{\mathbf{x}} \approx \sum_{l=1}^L w_l\,f(\hat{\mathbf{x}}_l)$$

> [!info] Exact integration
> For linear FEM: element stiffness $\mathbf{A}_K$ involves $\nabla\lambda_i \cdot \nabla\lambda_j$ (constant on $K$) → exact with 1-point quadrature. Element mass $\mathbf{M}_K$ involves $\lambda_i\,\lambda_j$ (quadratic) → exact with 3-point midpoint rule.

---

**Problems:** 2-8, 2-9 | **Related:** [[Triangular-Linear-FEM-2D]], [[Parametric-FEM]], [[Assembly-Algorithm]]
