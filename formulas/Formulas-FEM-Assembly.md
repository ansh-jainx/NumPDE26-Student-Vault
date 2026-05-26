---
tags: [formulas, chapter-2, FEM, element-matrices, assembly, quick-reference]
---

# Quick Reference: FEM Element Matrices & Assembly

---

## 1D Linear FEM (Uniform Mesh, Step $h$)

**Element stiffness** (interval $[x_{k-1}, x_k]$):

$$\mathbf{A}_e = \frac{1}{h}\begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$$

**Element mass:**

$$\mathbf{M}_e = \frac{h}{6}\begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$

**Global stiffness** ($N$ interior nodes): $\mathbf{A} = \frac{1}{h}\,\mathrm{tridiag}(-1, 2, -1)$

**Global mass:** $\mathbf{M} = \frac{h}{6}\,\mathrm{tridiag}(1, 4, 1)$

---

## 2D Linear FEM on Triangle $K$

Vertices $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$. Barycentric coordinates $\lambda_1, \lambda_2, \lambda_3$.

**Area:** $|K| = \frac{1}{2}|(\mathbf{a}_2 - \mathbf{a}_1) \times (\mathbf{a}_3 - \mathbf{a}_1)|$

**Gradients of barycentric coordinates:**

$$\nabla\lambda_i \text{ are constant on } K, \qquad \mathbf{G}_K = \begin{pmatrix} \nabla\lambda_1 & \nabla\lambda_2 & \nabla\lambda_3 \end{pmatrix} \in \mathbb{R}^{2\times 3}$$

Lecture helper `gradbarycoordinates` (Code 2.4.5.11) returns this $2 \times 3$ matrix (columns = gradients); it is not a public LehrFEM++ API symbol.

**Element stiffness (Eq. 2.4.5.12):**

$$(\mathbf{A}_K)_{ij} = |K|\,\nabla\lambda_i \cdot \nabla\lambda_j \qquad \Leftrightarrow \qquad \mathbf{A}_K = |K|\,\mathbf{G}_K^T\,\mathbf{G}_K$$

**Element mass:**

$$(\mathbf{M}_K)_{ij} = |K| \cdot \begin{cases} 1/6 & i = j \\ 1/12 & i \neq j \end{cases} \qquad \Leftrightarrow \qquad \mathbf{M}_K = \frac{|K|}{12}(\mathbf{I} + \mathbf{1}\mathbf{1}^T)$$

---

## Gradient Transformation (Lemma 2.8.3.10)

Affine map $\Phi_K: \hat{K} \to K$, $\mathbf{x} = \mathbf{a}_1 + \mathbf{F}_K\hat{\mathbf{x}}$:

$$\nabla_{\mathbf{x}} u = \mathbf{F}_K^{-T}\,\nabla_{\hat{\mathbf{x}}}\hat{u}$$

$$\int_K g\,\mathrm{d}\mathbf{x} = |\det \mathbf{F}_K| \int_{\hat{K}} g \circ \Phi_K\,\mathrm{d}\hat{\mathbf{x}}$$

---

## Assembly Pseudocode

```
for each cell K in mesh:
    A_K = ElementMatrixProvider.Eval(K)
    for (i_local, j_local) in local DOF pairs:
        I = DofHandler.GlobalDofIndices(K)[i_local]
        J = DofHandler.GlobalDofIndices(K)[j_local]
        A_global[I, J] += A_K[i_local, j_local]
```

---

## LehrFEM++ Cheat Sheet

| Task | Code |
|------|------|
| Stiffness matrix | `ReactionDiffusionElementMatrixProvider(fe_space, mf_alpha, mf_zero)` |
| Mass matrix | `ReactionDiffusionElementMatrixProvider(fe_space, mf_zero, mf_gamma)` |
| Load vector | `ScalarLoadElementVectorProvider(fe_space, mf_f)` |
| Boundary mass | `MassEdgeMatrixProvider(fe_space, mf_c, bd_selector)` |
| Assemble matrix | `AssembleMatrixLocally(0, dofh, dofh, provider, A_COO)` |
| Assemble vector | `AssembleVectorLocally(0, dofh, provider, phi)` |
| Flag boundary | `auto bd = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p)` |
| Fix Dirichlet | `FixFlaggedSolutionComponents(selector, A_COO, phi)` |

---

## Essential BC Treatment

After full assembly of $\mathbf{A}$ and $\boldsymbol{\varphi}$:

For each boundary DOF $i$ with $u_i = g_i$:
1. $\boldsymbol{\varphi} \mathrel{-}= g_i \cdot \mathbf{A}_{:,i}$ (subtract column contribution)
2. Set row $i$ and column $i$ of $\mathbf{A}$ to zero
3. Set $\mathbf{A}_{ii} = 1$, $\boldsymbol{\varphi}_i = g_i$
