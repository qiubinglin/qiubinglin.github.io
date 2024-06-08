---
layout:     post
title:      "Lagrange Multiplier"
date:       2024-04-30 17:38:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
---

# Lagrange multiplier
The basic idea is to convert a constrained problem into a form such that the derivative test of an unconstrained problem can still be applied.

Consider the following optimization problem
$$
    min \quad f(x)
    \\
    subjects \; to \quad g_i(x) = 0
$$
The Lagrange function is
$$
    \mathcal{L}(x, \lambda) = f(x) + \lambda^T g(x)
$$
where
$$
    g(x) = \begin{bmatrix}
        g_0(x) \\
        ... \\
        g_i(x) \\
        ...
    \end{bmatrix}
$$
and $\lambda$ is so-called Lagrange multiplier.

Then the optimal vector $x$ of $\mathcal{L}$ satisfies
$$
    \triangledown_x \mathcal{L}(x, \lambda) = 0 \quad and \quad g(x) = 0
$$

# KKT conditions
Extend the optimization problem with some inequality constraints as follow
$$
    min \quad f(x)
    \\
    subjects \; to \quad g_i(x) = 0
    \\
    subjects \; to \quad h_i(x) \leq 0
$$
then the Lagrange function would be
$$
    \mathcal{L}(x, \mu, \lambda) = f(x) + \lambda^T g(x) + \mu^T h(x)
    \\
    = f(x) + \alpha \begin{pmatrix}
        g(x)
        \\
        h(x)
    \end{pmatrix}
$$

## Karush–Kuhn–Tucker theorem
***(Sufficiency condition)***
If $(x_0, \alpha_0)$ is a saddle point of $\mathcal{L}(x, \alpha)$ and $\mu \geq 0$, then $x_0$ is the optimal vector for the optimization problem.

***(Necessity condition)***
Suppose that $f(x)$ and $h_i(x)$ are convex and that there exists $x_0$ such that $h_i(x_0) < 0$. Then with an optimal vector $x^*$ for the above problem there is associated a vector $\alpha^*$ satisfying $\mu^* \geq 0$ and $(x^*, \alpha^*)$ is saddle point.

### Proofs

# References
[https://en.wikipedia.org/wiki/Lagrange_multiplier](https://en.wikipedia.org/wiki/Lagrange_multiplier)

[https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions](https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions)