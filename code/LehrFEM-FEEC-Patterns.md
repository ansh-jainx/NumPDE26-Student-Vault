---
tags: [code, LehrFEM, FEEC, Whitney, Maxwell, magnetostatics]
---

# LehrFEM++ FEEC Patterns

> [!note] Illustrative snippets
> Patterns below follow LehrFEM++ layout; always compare with the **NPDERepo** mastersolution for the homework you are solving. Example folders: `MagStat2D`, `MaxwellEvlTM`, `HodgeLaplacian2D`.

---

## 1. Mesh incidence and cochain operators

For Problem **13-1** (`IncidenceMatrices` in this NPDERepo snapshot), build oriented incidence matrices between vertices, edges, and faces.

```cpp
// Schematic only (IncidenceMatrices mastersolution uses integer incidence)
Eigen::SparseMatrix<int> D0; // edges x vertices
Eigen::SparseMatrix<int> D1; // faces x edges
// exactness check:
assert((D1 * D0).norm() == 0);
```

## 2. Whitney-type space usage

Use edge/face-associated basis functions where conformity requires $H(\mathrm{curl})$/$H(\mathrm{div})$, not scalar nodal spaces.

```cpp
// Pseudocode: choose FE space by field degree
// degree 0 -> nodal
// degree 1 -> edge based
// degree 2 -> face based
```

## 3. Semi-discrete EM wave system

Assemble mass-like and curl-coupling blocks:

$$\mathbf M_e \dot{\mathbf e} + \mathbf C^T \mathbf b = \mathbf f, \qquad
\mathbf M_b \dot{\mathbf b} - \mathbf C \mathbf e = \mathbf 0.$$

Use implicit timestepping for robustness (analogy to [[Timestepping-MOL]]).

## 4. Magnetostatics mixed block solve

For Problems **13-2/13-3**:

```cpp
// assemble A (curl-curl / material), B (gauge/divergence constraint)
// solve [A B^T; B 0] [a; p] = [f; 0]
```

Handle null-space/gauge as in Stokes pressure pinning.

## 5. Verification pattern

- Confirm discrete identity $\mathbf D_1\mathbf D_0 = 0$.
- Check energy decay/conservation according to model.
- On mesh refinement, verify expected first-order Whitney convergence in norm(s) stated by chapter theory.

---

**Related:** [[LehrFEM-Assembly-Patterns]], [[LehrFEM-Solver-Convergence-Patterns]], [[Whitney-Forms]], [[FEEC-EM-Waves-Problems]], [[Magnetostatics-Problems]]
