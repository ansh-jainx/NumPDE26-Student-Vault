---
tags: [chapter-1, boundary-conditions, essential, natural, exam-critical]
first_appears: "[[Week-02-Elliptic-BVPs-II]]"
---

# Essential vs Natural Boundary Conditions

**Reference:** §1.9

---

## Classification

| | Essential | Natural |
|---|-----------|---------|
| **What** | Conditions on $u$ itself | Conditions on $\nabla u \cdot \mathbf{n}$ (flux) |
| **Examples** | Dirichlet: $u = g$ | Neumann: $\kappa\nabla u \cdot \mathbf{n} = h$, Robin |
| **How imposed** | Built into the function space $V$, $V_0$ | Emerge from integration by parts (Green's formula) |
| **FEM treatment** | Modify system after assembly ([[Essential-BC-Treatment]]) | Automatically satisfied by the variational formulation |
| **If forgotten** | Wrong solution (missing constraint) | Homogeneous Neumann imposed by default |

> [!tip] Default = homogeneous Neumann
> If you don't impose any BC on a boundary segment, the variational formulation automatically enforces $\nabla u \cdot \mathbf{n} = 0$ (zero flux). This is why Neumann BCs are called "natural."

## Green's First Formula (Thm 1.5.2.7)

The tool that separates essential from natural:

$$\int_\Omega (-\Delta u)\,v\,\mathrm{d}\mathbf{x} = \int_\Omega \nabla u \cdot \nabla v\,\mathrm{d}\mathbf{x} - \int_{\partial\Omega} (\nabla u \cdot \mathbf{n})\,v\,\mathrm{d}S$$

The boundary integral $\int_{\partial\Omega} (\nabla u \cdot \mathbf{n})\,v\,\mathrm{d}S$ is where natural BCs enter. If $v = 0$ on $\Gamma_D$ (test function for Dirichlet BC), this integral vanishes on $\Gamma_D$.

---

**Problems:** 1-6, 1-8, 1-9 | **Exams:** Midterm 0-1 appears in multiple years with changing emphasis | **Related:** [[Boundary-Conditions-Elliptic]], [[Essential-BC-Treatment]]
