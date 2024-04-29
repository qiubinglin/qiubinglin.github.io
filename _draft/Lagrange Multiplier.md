---
layout:     post
title:      "Lagrange Multiplier"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
---

# Lagrange multiplier
The basic idea is to convert a constrained problem into a form such that the derivative test of an unconstrained problem can still be applied.

Consider the following optimization problem
$$
    minimize \quad f(x)
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

Then the optimization target is to find the stationary points of $\mathcal{L}$ that satisfies
$$
    \triangledown_x \mathcal{L} = 0 \quad and \quad g(x) = 0
$$

# References
[https://en.wikipedia.org/wiki/Lagrange_multiplier](https://en.wikipedia.org/wiki/Lagrange_multiplier)