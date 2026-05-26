---
tags: [chapter-2, FEM, 2D, triangular, barycentric, exam-critical]
first_appears: "[[Week-03-FEM-I]]"
---

# Triangular Linear FEM in 2D

**Reference:** §2.4

---

## Setup

Triangulation $\mathcal{M}$ of $\Omega \subset \mathbb{R}^2$. On each triangle $K$ with vertices $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$:

## Barycentric Coordinates

$$\mathbf{x} = \lambda_1\,\mathbf{a}_1 + \lambda_2\,\mathbf{a}_2 + \lambda_3\,\mathbf{a}_3, \qquad \lambda_1 + \lambda_2 + \lambda_3 = 1$$

The local basis functions on $K$ are $b_i^K = \lambda_i$ (linear, $\lambda_i(\mathbf{a}_j) = \delta_{ij}$).

## Gradients

$$\nabla\lambda_i = \frac{1}{2|K|}\,\mathbf{n}_i$$

where $\mathbf{n}_i$ is the inward-pointing normal to the edge opposite vertex $\mathbf{a}_i$, scaled by edge length. Collect into gradient matrix $\mathbf{G}_K \in \mathbb{R}^{2 \times 3}$: column $i$ = $\nabla\lambda_i$ (matching lecture Code 2.4.5.11 `gradbarycoordinates`; this is not a public LehrFEM++ API symbol).

## Element Matrices

**Element stiffness (Eq. 2.4.5.12):**

$$(\mathbf{A}_K)_{ij} = |K|\,\nabla\lambda_i \cdot \nabla\lambda_j \qquad \Leftrightarrow \qquad \mathbf{A}_K = |K|\,\mathbf{G}_K^T\,\mathbf{G}_K$$

**Element mass:**

$$(\mathbf{M}_K)_{ij} = \int_K \lambda_i\,\lambda_j\,\mathrm{d}\mathbf{x} = \frac{|K|}{12}(1 + \delta_{ij})$$

Compact: $\mathbf{M}_K = \frac{|K|}{12}(\mathbf{1}\mathbf{1}^T + \mathbf{I})$

> [!warning] Area formula
> $|K| = \frac{1}{2}|(\mathbf{a}_2 - \mathbf{a}_1) \times (\mathbf{a}_3 - \mathbf{a}_1)|$ (signed area from cross product of edge vectors).

---

**Problems:** 2-2, 2-9, 2-11 | **Exams:** Midterm 0-2 appears in several years (year-specific variants) | **Related:** [[Local-Computations]], [[Assembly-Algorithm]]
