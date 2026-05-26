---
tags: [problems, chapter-1, elliptic, variational, Sobolev]
---

# Elliptic BVP Theory Problems

Problems from Chapter 1 covering §1.2–§1.9: quadratic functionals, Sobolev spaces, variational formulations, boundary conditions, strong ↔ weak form.

All problems are **purely theoretical** (pen-and-paper) except 1-10 and 1-11 which have small code components.

---

## Problem 1-1: Quadratic Functionals

**Sections:** §1.2.3

**Concepts:** [[Quadratic-Minimization-Problem]]

**Setup:** Given several functionals $J: V_0 \to \mathbb{R}$, decide whether each is quadratic (per Def. 1.2.3.2), identify the bilinear form $a$ and linear form $\ell$, check positive (semi-)definiteness.

| What it tests |
|--------------|
| Recognizing quadratic structure $J(v) = \frac{1}{2}a(v,v) - \ell(v) + c$ |
| Extracting $a$, $\ell$ from a given functional |
| Positive definiteness → uniqueness of minimizer |

> [!tip] Key skill
> This is the foundation: every elliptic BVP reduces to minimizing a quadratic functional. Being fast at identifying $a$ and $\ell$ from a given energy expression is essential for exams.

> [!abstract] Solution gist
> **(a)** $J(v) = \int x^2|v+1|^2$: expand $|v+1|^2 = v^2 + 2v + 1$ → quadratic with $a(u,v) = 2\int x^2 uv$, $\ell(v) = -2\int x^2 v$, s.p.d. **(b)** $J(v) = \int v'v''$: integrate by parts to get $-\frac{1}{2}\int (v')^2$ plus boundary terms — not quadratic in general (boundary terms spoil symmetry). **(c)** $J(\mathbf{v}) = \sum (v_j - v_{j-1})^2$: expand → $\mathbf{A}$ is tridiagonal s.p.d. matrix, $\mathbf{b} = \mathbf{0}$. **(d)** $J(v) = \int |\mathbf{f}\cdot\nabla v - 1|^2$: expand → quadratic, $a(u,v) = 2\int (\mathbf{f}\cdot\nabla u)(\mathbf{f}\cdot\nabla v)$, s.p.s.d. **(e)** $J(v) = \int v\,\partial_{x_1}v$: not symmetric → not quadratic. **(f)** $J(v) = (\int(v+1))^2$: expand → $a(u,v) = 2(\int u)(\int v)$, s.p.s.d. (kernel = mean-zero functions). **(g)** Polarization identity: $a(u,v) = J(u+v) - J(u) - J(v) + J(0)$ — direct verification by expanding $J$.

---

## Problem 1-2: Linear Functionals on Sobolev Spaces

**Sections:** §1.2.3, §1.3, §1.9

**Concepts:** [[Sobolev-Spaces]], [[Lax-Milgram-Theorem]]

**Setup:** Study continuity of various linear functionals (point evaluation, integral, boundary trace) with respect to $H^1$-norms. Uses multiplicative trace inequality (Thm 1.9.0.10).

| What it tests |
|--------------|
| Continuity of functionals on $H^1(\Omega)$ |
| Cauchy-Schwarz and trace inequalities |
| Why point evaluation fails in $L^2$ but works in $H^1$ (1D) |

> [!abstract] Solution gist
> Four functionals on the unit disk: $\ell_1(v) = \int \mathbf{c}\cdot\nabla v$, $\ell_2(v) = \int v$, $\ell_3(v) = \int_{\partial\Omega} \nabla v \cdot \mathbf{n}$, $\ell_4(v) = \int v\frac{\mathbf{x}}{\|\mathbf{x}\|}$. **On $L^2$:** $\ell_1$ not continuous (involves $\nabla v$, not controlled by $L^2$ norm); $\ell_2$ continuous by Cauchy-Schwarz; $\ell_3$ not continuous (involves $\nabla v$ trace); $\ell_4$ continuous by Cauchy-Schwarz since $\frac{\mathbf{x}}{\|\mathbf{x}\|} \in L^\infty$. **On $H^1$:** $\ell_1$ yes (Cauchy-Schwarz on gradient term); $\ell_2$ yes (trivially); $\ell_3$ no — counterexample: $v_n(x) = \|x\|^{2n}/(2n)$, $|\ell_3(v_n)| \to \infty$ while $\|v_n\|_{H^1}$ stays bounded; $\ell_4$ yes (Cauchy-Schwarz). Tool: multiplicative trace inequality $\|u\|_{L^2(\partial\Omega)}^2 \leq C\|u\|_{L^2}\|u\|_{H^1}$.

---

## Problem 1-3: $L^\infty$-Norms Bounded by $H^1$-Seminorms in 1D

**Sections:** §1.3

**Concepts:** [[Sobolev-Spaces]]

**Setup:** Prove $\|u\|_{L^\infty} \leq C\,|u|_{H^1}$ in 1D. Uses fundamental theorem of calculus + Cauchy-Schwarz.

| What it tests |
|--------------|
| Sobolev embedding in 1D |
| Technique: "plug in definition, use Cauchy-Schwarz" |

> [!abstract] Solution gist
> For $u \in H^1_0(]a,b[)$: write $u(x) = \int_a^x u'(t)\,\mathrm{d}t$, apply Cauchy-Schwarz → $|u(x)|^2 \leq (x-a)\int_a^b |u'|^2 \leq (b-a)|u|_{H^1}^2$. Take supremum → $\|u\|_{L^\infty} \leq \sqrt{b-a}\,|u|_{H^1}$. Generalizations for $u(a) \neq 0$: use $u(x) = u(a) + \int_a^x u'$.

---

## Problem 1-4: A Poincaré-Type Inequality

**Sections:** §1.3, §1.8

**Concepts:** [[Sobolev-Spaces]]

**Setup:** Prove a variant of the Poincaré-Friedrichs inequality using mean-value constraints instead of boundary conditions. Related to Thm 1.3.4.17 and Thm 1.8.0.20.

| What it tests |
|--------------|
| Poincaré-Friedrichs inequality and its variants |
| When $\lvert\cdot\rvert_{H^1}$ is equivalent to $\lVert\cdot\rVert_{H^1}$ |

> [!abstract] Solution gist
> Prove $\|u\|_{H^1}^2 \leq C\,|u|_{H^1}^2$ when $\int_\Omega u = 0$ (mean-zero constraint). Standard Poincaré-Friedrichs: if $u$ has zero boundary trace or zero mean, then $\|u\|_{L^2} \leq C_\Omega\,|u|_{H^1}$. Therefore $\|u\|_{H^1}^2 = \|u\|_{L^2}^2 + |u|_{H^1}^2 \leq (1 + C_\Omega^2)|u|_{H^1}^2$. The converse is trivial → norms are equivalent on the constrained subspace.

---

## Problem 1-5: A Second-Order Elliptic Transmission Problem in 1D

**Sections:** §1.5.1

**Concepts:** [[Linear-Variational-Problem]], [[Sobolev-Spaces]]

**Setup:** Variational problem with discontinuous coefficient (transmission condition at interface). Derive strong form piecewise, identify jump condition.

| What it tests |
|--------------|
| Deriving strong PDE from variational form (§1.5.1 technique) |
| Transmission/interface conditions from integration by parts |
| Coercivity proof using Poincaré-Friedrichs |

> [!warning] Common mistake
> The coefficient $\kappa$ jumps at the interface → the PDE holds piecewise, and the variational form encodes a flux continuity condition at the jump.

> [!abstract] Solution gist
> Variational form with $\kappa(x)$ piecewise constant. Integration by parts on each sub-interval → strong form $-(\kappa u')' = f$ on each piece. At interface $x_0$: choosing test functions supported near $x_0$ yields the transmission condition $[\kappa u']_{x_0} = 0$ (flux continuity). Coercivity: $a(v,v) = \int \kappa|v'|^2 \geq \kappa_{\min}|v|_{H^1}^2$, then Poincaré-Friedrichs if $v(0) = 0$ or $v(1) = 0$.

---

## Problem 1-6: Heat Conduction with Non-Local Boundary Conditions

**Sections:** §1.5, §1.8

**Concepts:** [[Boundary-Conditions-Elliptic]], [[Essential-vs-Natural-BCs]], [[Linear-Variational-Problem]]

**Setup:** Variational problem where the boundary condition involves an integral (non-local). Derive the associated strong form and BCs.

| What it tests |
|--------------|
| Non-standard variational formulations |
| Extracting BCs hidden in the variational form |

> [!abstract] Solution gist
> Non-local BC: the variational form includes a term like $\alpha\left(\int_{\partial\Omega} u\right)\left(\int_{\partial\Omega} v\right)$ coupling boundary values globally. Integration by parts → strong form $-\Delta u = f$ in $\Omega$, with a non-local Neumann-type BC: $\nabla u \cdot \mathbf{n} = g - \alpha\int_{\partial\Omega} u$. The bilinear form remains coercive because the non-local boundary term is s.p.s.d.

---

## Problem 1-7: A Second-Order BVP for Vector Fields

**Sections:** §1.5

**Concepts:** [[Linear-Variational-Problem]]

**Setup:** Extend the scalar BVP framework to vector-valued unknowns. Derive strong form from a variational problem on $[H^1(\Omega)]^d$.

| What it tests |
|--------------|
| Vector-valued variational problems |
| Systems of PDEs from variational formulations |

> [!abstract] Solution gist
> Vector-valued unknown $\mathbf{u} \in [H^1(\Omega)]^d$. Variational form on product space: integration by parts component-wise → system of PDEs. For strain-energy type: $a(\mathbf{u}, \mathbf{v}) = \int_\Omega \varepsilon(\mathbf{u}):\varepsilon(\mathbf{v})$ → strong form involves $-\text{div}(\varepsilon(\mathbf{u})) = \mathbf{f}$ (linearized elasticity). BCs from boundary integrals in the bilinear form.

---

## Problem 1-8: A Coupled Reaction-Diffusion Problem

**Sections:** §1.8

**Concepts:** [[Linear-Variational-Problem]], [[Lax-Milgram-Theorem]]

**Setup:** System of two coupled elliptic PDEs. Identify bilinear form on product space, check coercivity.

| What it tests |
|--------------|
| Coupled systems in variational form |
| Coercivity on product spaces |

> [!abstract] Solution gist
> Two unknowns $u, w$ with coupling terms. Product space $V = H^1 \times H^1$, test with $(v, z)$. Coercivity on product space: need $a((u,w),(u,w)) \geq \alpha(\|u\|_{H^1}^2 + \|w\|_{H^1}^2)$. Often use Young's inequality $2|ab| \leq \epsilon a^2 + \frac{1}{\epsilon}b^2$ to handle cross-terms. The reaction (zeroth-order) coupling must not destroy coercivity of the diffusion terms.

---

## Problem 1-9: Second-Order Elliptic BVP from Weak Formulations

**Sections:** §1.5, §1.7, §1.9

**Concepts:** [[Essential-vs-Natural-BCs]], [[Boundary-Conditions-Elliptic]], [[Linear-Variational-Problem]]

**Setup:** Given a variational problem, derive the strong PDE and identify what boundary conditions are imposed (essential vs natural).

| What it tests |
|--------------|
| Reverse direction: variational form → strong form + BCs |
| Identifying essential vs natural BCs from the test/trial spaces |

> [!abstract] Solution gist
> Given variational problem → integrate by parts "backwards" to extract strong PDE. The test space tells you which BCs are essential (built into the space, e.g., $H^1_0$ → Dirichlet) vs natural (emerge from integration by parts, e.g., Neumann/Robin). If test functions vanish on $\Gamma_D$ → Dirichlet is essential there. Boundary integrals that remain after IBP → natural BCs.

---

## Problem 1-10: From Boundary Value Problems to Variational Problems

**Code folder:** `—` | **Sections:** §1.4, §1.7, §1.9

**Concepts:** [[Essential-vs-Natural-BCs]], [[Boundary-Conditions-Elliptic]], [[Linear-Variational-Problem]], [[Lax-Milgram-Theorem]]

**Setup:** Given several BVPs with various BCs, derive the variational formulation. Small code component for verification.

| What it tests |
|--------------|
| Forward direction: strong form + BCs → variational form |
| Choosing correct trial/test spaces for each BC type |
| Exam-critical: forward BVP → variational (common midterm 0-1 style) |

> [!warning] Exam alert
> Closest template for midterm **0-1** chain (2021–2026). Deep dive: [[Exam-Deep-Elliptic-Weak-Form]] | Bank: [[Exam-Master-Bank#Ch1]]

> [!abstract] Solution gist
> Recipe: (1) Multiply PDE by test function $v$. (2) Integrate over $\Omega$. (3) Integration by parts on second-order terms → $\int_\Omega \nabla u \cdot \nabla v$ + boundary integral. (4) Substitute BC into boundary integral: Dirichlet → impose on trial space; Neumann $\nabla u \cdot \mathbf{n} = g$ → becomes $\int_{\partial\Omega} gv$; Robin $\nabla u \cdot \mathbf{n} + cu = g$ → split into bilinear ($c\int uv$) and linear ($\int gv$). (5) Identify $a(u,v)$ and $\ell(v)$, state trial/test spaces. Common pitfall: forgetting that Dirichlet data enters via a *lift* — trial space is $u_0 + V_0$ where $u_0$ satisfies the Dirichlet BC.

---

## Problem 1-11: Strong and Weak Form of Elliptic BVPs

**Code folder:** `—` | **Sections:** §1.5, §1.9

**Concepts:** [[Essential-vs-Natural-BCs]], [[Boundary-Conditions-Elliptic]], [[Linear-Variational-Problem]]

> [!warning] Exam alert
> **2026 Midterm 0-1** mixed BC variant. See [[Exam-Deep-Elliptic-Weak-Form#2026 Midterm 0-1]].

**Setup:** Both directions: strong → weak and weak → strong. Multiple BVPs with Dirichlet, Neumann, and Robin BCs.

| What it tests |
|--------------|
| Bidirectional conversion strong ↔ weak form |
| All three BC types in one problem |

> [!abstract] Solution gist
> Practice problem combining all directions. Strong → weak: follow recipe from 1-10. Weak → strong: apply Green's formula in reverse — any term involving $\nabla v$ originated from IBP of a second-order operator. Boundary integrals that remain after IBP reveal natural BCs. Each BC type changes what goes where: Dirichlet → trial/test space restriction; Neumann → RHS linear form; Robin → both bilinear form and linear form get boundary terms.

---

---

## Exam mapping (midterm Problem 0-1)

| Year | Topic | Closest problems |
|------|-------|------------------|
| **2026** | Reformulating elliptic variational problem | **1-10**, **1-11** |
| **2023** | BVP → variational problems | **1-10** |
| **2022** | BVP, variational, quadratic minimization | **1-1**, **1-10** |
| **2021** | Elliptic BVP from weak formulations | **1-9** |

> [!info] Not every midterm uses the same template. **2024** Midterm 0-1 was convection bilinear form (Ch 10). There is no classic 2025 midterm in the course PDF set.
