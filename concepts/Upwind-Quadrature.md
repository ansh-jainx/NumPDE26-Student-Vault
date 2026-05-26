---
tags: [chapter-10, upwind, quadrature, convection, exam-critical]
first_appears: "[[Week-08-Convection-Diffusion]]"
---

# Upwind Quadrature

**Reference:** §10.2.2.1

---

## Idea

Replace exact integration of the convection term $\int_K (\mathbf{v} \cdot \nabla u)\,w\,\mathrm{d}\mathbf{x}$ by a **quadrature rule** that evaluates the integrand only at **upstream** nodes (relative to flow direction $\mathbf{v}$).

On triangle $K$ with vertices $\mathbf{x}_i$, $\mathbf{x}_j$, $\mathbf{x}_k$: for node $i$, the **upstream triangle** $K_{u,i}$ is the sub-triangle where flow enters toward $\mathbf{x}_i$. Upwind quadrature uses:

$$\int_K (\mathbf{v} \cdot \nabla u)\,w\,\mathrm{d}\mathbf{x} \approx |K|\,(\mathbf{v} \cdot \nabla u)(\mathbf{x}_i)\,w(\mathbf{x}_i) \cdot \omega_i$$

with weights from upstream geometry.

## Properties

- Yields a **non-symmetric** element matrix (like the continuous form)
- **Stable** for convection-dominated problems — no spurious oscillations as $\varepsilon \to 0$
- Combined with diffusive Galerkin term: upwind quadrature on acute meshes (§10.2.2.11; Exp. 10.2.2.20)

> [!tip] Exam relevance
> **2024 Endterm 0-2** asks for upwind quadrature discretization of a convection-diffusion BVP. Know how to identify upstream nodes and write element contributions.

## LehrFEM++ connection

Standard assembly uses `ConvBLFMatrixProvider` for the continuous convection form (Problem **2-17**). Upwind quadrature modifies quadrature point selection — see [[LehrFEM-Convection-Patterns]].

---

**Problems:** 10-2, 10-8 | **Related:** [[Convection-Diffusion-Modeling]], [[Singular-Perturbation]], [[Streamline-Diffusion]]
