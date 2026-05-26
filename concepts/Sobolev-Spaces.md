---
tags: [chapter-1, function-spaces, Sobolev, Poincare, exam-critical]
first_appears: "[[Week-01-Elliptic-BVPs-I]]"
---

# Sobolev Spaces

**Reference:** §1.3.3–§1.3.4

---

## Key Spaces

| Space | Definition | Norm |
|-------|-----------|------|
| $L^2(\Omega)$ | Square-integrable functions | $\|u\|_0 = \left(\int_\Omega u^2\,\mathrm{d}\mathbf{x}\right)^{1/2}$ |
| $H^1(\Omega)$ | Functions with square-integrable weak gradient | $\|u\|_{H^1}^2 = \|u\|_0^2 + \|\nabla u\|_0^2$ |
| $H_0^1(\Omega)$ | $H^1$ functions with zero trace on $\partial\Omega$ | $|u|_{H^1} = \|\nabla u\|_0$ (by Poincaré-Friedrichs) |

**Seminorm vs norm:** $|u|_{H^1} = \|\nabla u\|_0$ is only a seminorm on $H^1$ (constant functions have zero seminorm), but is a **full norm on $H_0^1$** — equivalent to $\|\cdot\|_{H^1}$ by Poincaré-Friedrichs. The lecture notes (Def. 1.3.4.3) define $H_0^1$ with this seminorm as its norm.

## Poincaré-Friedrichs Inequality (Thm 1.3.4.17)

$$\|u\|_0 \leq \mathrm{diam}(\Omega)\,\|\nabla u\|_0 \qquad \forall u \in H_0^1(\Omega)$$

> [!warning] This inequality is fundamental
> It proves that $|\cdot|_{H^1}$ is a norm on $H_0^1$, enables coercivity proofs for [[Lax-Milgram-Theorem]], and provides the decay rate $\gamma$ in [[Stability-Parabolic-Evolution]].

## Trace Operator (Cor. 1.3.4.7)

In 1D: point evaluation $u(x_0)$ is well-defined for $u \in H^1$. In higher dimensions: boundary values $u|_{\partial\Omega}$ exist in a trace sense ($u \in H^1 \Rightarrow u|_{\partial\Omega} \in L^2(\partial\Omega)$).

## Role in Variational Problems

- **Dirichlet BC** ($u = 0$ on $\partial\Omega$): work in $H_0^1(\Omega)$
- **Neumann/Robin BC**: work in $H^1(\Omega)$ (no restriction on boundary values)
- Sobolev spaces are Hilbert spaces → [[Quadratic-Minimization-Problem]] has a unique minimizer

---

**Problems:** 1-5 | **Related:** [[Linear-Variational-Problem]], [[Spatial-Variational-Formulation-Parabolic]], [[Boundary-Conditions-Elliptic]]
