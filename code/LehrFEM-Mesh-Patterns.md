---
tags: [code, LehrFEM, mesh, entities, iteration, boundary]
---

# LehrFEM++ Mesh & Entity Patterns

---

## 1. Entity Iteration

```cpp
auto mesh_p = /* ... */;

// All cells (co-dim 0)
for (const lf::mesh::Entity* cell : mesh_p->Entities(0)) {
  // cell->RefEl()     — lf::base::RefEl::kTria or kQuad
  // cell->Geometry()  — geometry object (coordinates, Jacobian)
}

// All edges (co-dim 1)
for (const lf::mesh::Entity* edge : mesh_p->Entities(1)) { /* ... */ }

// All nodes (co-dim 2)
for (const lf::mesh::Entity* node : mesh_p->Entities(2)) {
  Eigen::Vector2d coords = lf::geometry::Corners(*node->Geometry()).col(0);
}
```

---

## 2. Incidence: Sub-Entities of a Cell

```cpp
const lf::mesh::Entity& cell = /* ... */;

// Edges of a cell
auto edges = cell.SubEntities(1); // span of Entity*

// Nodes of a cell
auto nodes = cell.SubEntities(2);
int n_nodes = cell.RefEl().NumNodes(); // 3 for triangle, 4 for quad

// Vertex coordinates
Eigen::MatrixXd corners = lf::geometry::Corners(*cell.Geometry());
// corners is 2 x n_nodes, each column = vertex
```

---

## 3. Boundary Detection

```cpp
// Flag all entities on boundary
auto bd_flags = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p);
// bd_flags is a CodimMeshDataSet<bool> — query with bd_flags(*entity)

// Check if specific edge is on boundary
for (const lf::mesh::Entity* edge : mesh_p->Entities(1)) {
  if (bd_flags(*edge)) {
    // This edge is on ∂Ω
  }
}

// Boundary selector for edge matrix providers
auto bd_selector = [&bd_flags](const lf::mesh::Entity& edge) -> bool {
  return bd_flags(edge);
};
```

---

## 4. DOF Handling

```cpp
const lf::assemble::DofHandler& dofh = fe_space->LocGlobMap();

// Total DOFs
int N = dofh.NumDofs();

// Global DOF indices for a cell
auto local2global = dofh.GlobalDofIndices(cell);
// local2global[i] = global index of local DOF i

// Interior DOFs of an entity
auto interior_dofs = dofh.InteriorGlobalDofIndices(entity);
```

| FE degree | DOFs per node | DOFs per edge | DOFs per cell |
|:-:|:-:|:-:|:-:|
| $p=1$ | 1 | 0 | 0 |
| $p=2$ | 1 | 1 | 0 |

---

## 5. Geometry: Jacobian and Volume

```cpp
const lf::geometry::Geometry& geo = *cell.Geometry();

// Evaluate Jacobian at reference point(s)
Eigen::MatrixXd ref_pts(2, 1);  // one point in 2D ref element
ref_pts << 0.33, 0.33;          // barycenter of reference triangle
auto jac = geo.Jacobian(ref_pts);  // 2x2 matrix (for affine: constant)

// Integration element |det F_K| at quadrature points
auto int_el = geo.IntegrationElement(ref_pts);  // vector of |det F_K|

// Cell volume
double vol = lf::geometry::Volume(geo);
```

---

## 6. Mesh Data Sets

```cpp
// Store per-cell data
lf::mesh::utils::CodimMeshDataSet<double> cell_data(mesh_p, 0, 0.0);
for (const lf::mesh::Entity* cell : mesh_p->Entities(0)) {
  cell_data(*cell) = compute_something(*cell);
}

// Store per-node data
lf::mesh::utils::CodimMeshDataSet<Eigen::Vector2d> node_coords(mesh_p, 2);
```

---

## 7. Mesh Generation

```cpp
// From Gmsh file
auto mesh_factory = std::make_unique<lf::mesh::hybrid2d::MeshFactory>(2);
lf::io::GmshReader reader(std::move(mesh_factory), "domain.msh");
auto mesh_from_gmsh = reader.mesh();

// Built-in test mesh
auto mesh_test = lf::mesh::test_utils::GenerateHybrid2DTestMesh(0);

// Structured mesh on [0,1]^2
auto mesh_structured = lf::mesh::test_utils::GenerateHybrid2DTestMesh(3, 1.0 / N);
```

---

## 8. VTK Output

```cpp
lf::io::VtkWriter vtk_writer(mesh_p, "output.vtk");
// Write FE solution
auto mf_sol = lf::fe::MeshFunctionFE(fe_space, mu);
vtk_writer.WritePointData("u_h", mf_sol);
```

---

**Related:** [[Mesh-Data-Structures]], [[Assembly-Algorithm]], [[Local-Computations]]
