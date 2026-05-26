---
tags: [chapter-2, mesh, LehrFEM, data-structures]
first_appears: "[[Week-04-FEM-II]]"
---

# Mesh Data Structures

**Reference:** §2.7.1–§2.7.3

---

## Mesh Entities

A 2D mesh $\mathcal{M}$ consists of entities at three co-dimensions:

| Co-dim | Entity | Example |
|--------|--------|---------|
| 0 | Cells (triangles, quads) | The elements $K$ |
| 1 | Edges (segments) | Shared between adjacent cells |
| 2 | Nodes (vertices) | Mesh points $\mathbf{a}_i$ |

**Incidence relations:** which entities are sub-entities of which (e.g., which nodes belong to a cell, which cells share an edge).

## LehrFEM++ Classes

| Class | Role |
|-------|------|
| `lf::mesh::Mesh` | The mesh object, stores all entities and incidence |
| `lf::mesh::Entity` | A single entity (cell, edge, or node) |
| `lf::mesh::hybrid2d::MeshFactory` | Builder for creating meshes |
| `lf::mesh::utils::flagEntitiesOnBoundary` | Mark boundary entities for BC treatment |

## DOF Handler

`lf::assemble::UniformFEDofHandler` manages the **local-to-global DOF mapping** (LehrFEM++ also exposes this via `LocGlobMap()` on the handler):

- For each cell $K$: maps local DOF indices $(0, 1, \ldots)$ to global DOF indices
- For linear FEM ($p=1$): DOFs are at nodes only
- For quadratic FEM ($p=2$): DOFs at nodes + edge midpoints

> [!tip] DOF numbering matters for assembly
> The DOF handler determines how element matrix entries scatter into the global [[Galerkin-Matrix]]. See [[Assembly-Algorithm]].

---

**Problems:** 2-6, 2-14 | **Related:** [[Assembly-Algorithm]], [[Local-Computations]]
