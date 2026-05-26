---
tags: [chapter-10, singular-perturbation, Peclet, exam-critical]
first_appears: "[[Week-08-Convection-Diffusion]]"
---

# Singular Perturbation

**Reference:** §10.2.1 (Def. 10.2.1.9)

---

## Definition

A BVP depending on $\varepsilon \approx \varepsilon_0$ is **singularly perturbed** if the limit problem as $\varepsilon \to 0$ is **not compatible** with the boundary conditions.

For (10.2.0.1): the limit $\varepsilon \to 0$ gives a **hyperbolic** transport problem $ \mathbf{v} \cdot \nabla u = f$, while the full problem is **elliptic**. Type change at $\varepsilon = 0$.

## Peclet Number

$$\mathrm{Pe} = \frac{\|\mathbf{v}\|_{L^\infty}\,L}{\varepsilon}$$

where $L = \mathrm{diam}(\Omega)$. Large Pe $\Rightarrow$ convection-dominated.

| Regime | Behavior |
|--------|----------|
| $\mathrm{Pe} \ll 1$ | Diffusion-dominated — standard Galerkin works |
| $\mathrm{Pe} \gg 1$ | Convection-dominated — layers, oscillations, need stabilization |

## Numerical consequences

> [!warning] Why standard FEM fails
> For large Pe, Galerkin FEM produces **spurious oscillations** (pollution, overshoots). The discrete problem mimics an unstable centered scheme for advection.

**Remedies:** [[Upwind-Quadrature]], [[Streamline-Diffusion]] (SUPG).

## Boundary layers

Internal or boundary layers of width $O(\varepsilon)$ where $u$ changes rapidly. Mesh must resolve layers, or use stabilization.

---

**Problems:** 10-2, 10-6, 10-7 | **Related:** [[Convection-Diffusion-Modeling]], [[Formulas-Convection-Diffusion]]
