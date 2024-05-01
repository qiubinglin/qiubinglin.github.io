---
layout:     post
title:      "Lagrange Dual Problem"
date:       2024-05-01 15:52:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
---

# Primal problem
Consider a possibly non-convex optimization problem $p^*$
$$
    min \quad f(x)
    \\
    subjects \; to \quad g_i(x) \leq 0
$$

# Dual problem
The Lagrange function
$$
    \mathcal{L}(x, \lambda) = f(x) + \lambda^T g(x)
$$

For every feasible $x$ and every $\lambda \geq 0$, $f(x)$ is bounded below by $\mathcal{L}(x, \lambda)$
$$
    f(x) \geq \mathcal{L}(x, \lambda)
$$

The Lagrangian can be used to express the primal problem to an unconstrained one
$$
    p^* = \underset{x}{min} \; \underset{\lambda \geq 0}{max} \; \mathcal{L}(x, \lambda)
$$

The Lagrange dual function is defined as
$$
    G(\lambda) := \underset{x}{min} \; \mathcal{L}(x, \lambda)
$$
And we can define the Lagrange dual problem as
$$
    d^* := \max \; G(\lambda)
$$

***Theorem 1(Weak duality)*** For possibly non-convex problem, weak duality holds: $p^* \geq d^*$.

# KKT conditions

# References
Lagrange multiplier: [https://en.wikipedia.org/wiki/Lagrange_multiplier](https://en.wikipedia.org/wiki/Lagrange_multiplier)

[https://en.wikipedia.org/wiki/Duality_(optimization)](https://en.wikipedia.org/wiki/Duality_(optimization))

[https://people.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture7.pdf](https://people.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture7.pdf)

[https://palomar.home.ece.ust.hk/ELEC5470_lectures/slides_Lagrange_duality.pdf](https://palomar.home.ece.ust.hk/ELEC5470_lectures/slides_Lagrange_duality.pdf)