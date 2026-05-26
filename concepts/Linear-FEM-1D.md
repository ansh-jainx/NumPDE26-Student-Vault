---
tags: [chapter-2, FEM, 1D, tent-functions, tridiagonal]
first_appears: "[[Week-03-FEM-I]]"
---

# Linear FEM in 1D

**Reference:** §2.3

---

## Setup

BVP: $-u'' = f$ on $]a,b[$, $u(a) = u(b) = 0$.

Mesh: $N$ interior nodes $x_1 < x_2 < \cdots < x_N$ on $[a,b]$, with $x_0 = a$, $x_{N+1} = b$.

## Tent (Hat) Function Basis

$$b_i^h(x) = \begin{cases} \frac{x - x_{i-1}}{h_i} & x \in [x_{i-1}, x_i] \\ \frac{x_{i+1} - x}{h_{i+1}} & x \in [x_i, x_{i+1}] \\ 0 & \text{otherwise} \end{cases}$$

Each $b_i^h$ is piecewise linear, $b_i^h(x_j) = \delta_{ij}$ (nodal interpolation).

## Element Matrices (uniform mesh, $h_i = h$)

**Stiffness:** $\mathbf{A} = \frac{1}{h}\begin{pmatrix} 2 & -1 & & \\ -1 & 2 & -1 & \\ & \ddots & \ddots & \ddots \\ & & -1 & 2 \end{pmatrix}$

**Mass:** $\mathbf{M} = \frac{h}{6}\begin{pmatrix} 4 & 1 & & \\ 1 & 4 & 1 & \\ & \ddots & \ddots & \ddots \\ & & 1 & 4 \end{pmatrix}$

> [!tip] Element stiffness for one interval
> On interval $[x_{i-1}, x_i]$ of length $h$: local stiffness $= \frac{1}{h}\begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$, local mass $= \frac{h}{6}\begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$.

---

**Problems:** 2-1, 2-3, 2-4, 2-12 | **Related:** [[Triangular-Linear-FEM-2D]], [[Galerkin-Discretization]]
