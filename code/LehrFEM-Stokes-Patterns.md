---
tags: [code, LehrFEM, Stokes, mixed-FEM, Taylor-Hood]
---

# LehrFEM++ Stokes Patterns

---

## 1. Taylor-Hood Spaces

```cpp
// Velocity: quadratic Lagrangian
auto fe_space_u = std::make_shared<lf::uscalfe::FeSpaceLagrangeO2>(mesh_p);
// Pressure: linear Lagrangian  
auto fe_space_p = std::make_shared<lf::uscalfe::FeSpaceLagrangeO1>(mesh_p);

const auto& dofh_u = fe_space_u->LocGlobMap();
const auto& dofh_p = fe_space_p->LocGlobMap();
```

## 2. Block System Structure

$$\begin{pmatrix} \mathbf{A} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0} \end{pmatrix} \begin{pmatrix} \boldsymbol{\mu}_u \\ \boldsymbol{\mu}_p \end{pmatrix} = \begin{pmatrix} \boldsymbol{\varphi}_u \\ \mathbf{0} \end{pmatrix}$$

- $\mathbf{A}$: strain energy $\int_\Omega \mu\, D\mathbf{u} : D\mathbf{w}$ — vector-valued assembly
- $\mathbf{B}$: discrete divergence linking velocity DOFs to pressure DOFs
- Zero block: no pressure-pressure term

## 3. Assembly Sketch

```cpp
// 1. Assemble viscous stiffness A (vector-valued)
// 2. Assemble divergence matrix B (rectangular: n_u × n_p)
// 3. Form block matrix [A, B^T; B, 0]
// 4. Solve with block solver or Schur complement
```

## 4. Pressure Null-Space

Pure Neumann pressure is defined up to constants. Pin one pressure DOF or impose $\int_\Omega p_h = 0$.

## 5. Crouzeix-Raviart (Problem 2-14)

Non-conforming: edge DOFs for velocity, cell DOFs for $P_0$ pressure. Use `NonConformingCrouzeixRaviartFiniteElements` code folder pattern.

---

**Related:** [[LehrFEM-Assembly-Patterns]], [[Taylor-Hood-FEM]], [[Crouzeix-Raviart-FEM]], [[Stokes-Problems]]
