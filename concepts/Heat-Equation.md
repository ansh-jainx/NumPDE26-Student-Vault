---
tags: [chapter-9, parabolic, PDE, heat-equation, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Heat Equation

**Reference:** §9.2.1

---

## The PDE

$$\frac{\partial}{\partial t}(\rho\,u) - \operatorname{div}(\kappa\,\operatorname{grad}\,u) = f \quad \text{in } \Omega \times\,]0,T[$$

**Derived from:** energy conservation in control volumes + Fourier's law $\mathbf{j} = -\kappa\,\operatorname{grad}\,u$.

**Requires:** initial condition $u(\mathbf{x},0) = u_0(\mathbf{x})$ + spatial BCs (Dirichlet/Neumann/radiation) on $\partial\Omega \times\,]0,T[$.

> [!warning] Compatibility
> For Dirichlet data $g$: must have $g(\mathbf{x},0) = u_0(\mathbf{x})$ on $\partial\Omega$.

## Key Insight

An evolution PDE is an ODE in an infinite-dimensional function space — this motivates the [[Method-of-Lines]].

## 1D Exact Solution (§9.2.3.1)

On $]0,1[$ with homogeneous Dirichlet BCs: $u(x,t) = \sum_k \alpha_k \sin(k\pi x)\,e^{-\pi^2 k^2 t}$. High-frequency modes decay fastest — solutions smooth out.

---

**Problems:** [[Parabolic-Timestepping-Problems]] | **Next:** [[Spatial-Variational-Formulation-Parabolic]], [[Method-of-Lines]]
