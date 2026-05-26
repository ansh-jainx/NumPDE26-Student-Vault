---
tags: [chapter-12, Stokes, Crouzeix-Raviart, non-conforming]
first_appears: "[[Week-10-Stokes-II]]"
---

# Crouzeix-Raviart FEM

**Reference:** §12.3.5

---

## Element pair

| Field | Space | DOFs |
|-------|-------|------|
| Velocity | Non-conforming $P_1$ on edges (CR space) | 1 DOF per edge |
| Pressure | $P_0$ (piecewise constant) | 1 DOF per cell |

Velocity is **not** globally continuous — only edge midpoints match. Pressure is discontinuous across elements.

## Why stable

Another LBB-stable pair for Stokes. Often cheaper than Taylor-Hood (fewer DOFs for velocity in some regimes).

> [!info] Prior exposure
> Introduced in Problem **2-14** ([[FEM-Assembly-Implementation-Problems]]) and theory in **3-16** ([[FEM-Extensions-Advanced-Problems]]). Week 10 connects to Stokes saddle-point context.

## Trade-offs

| | Taylor-Hood | Crouzeix-Raviart |
|---|-------------|------------------|
| Velocity continuity | $H^1$-conforming | Non-conforming |
| Pressure | $P_1$ | $P_0$ |
| Implementation | Standard Lagrangian | Edge DOFs, special assembly |

---

**Problems:** 2-14, 3-16, 12-2 | **Related:** [[Taylor-Hood-FEM]], [[Lagrangian-FEM]], [[Pressure-Instability]]
