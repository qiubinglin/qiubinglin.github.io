---
layout:     post
title:      "Lagrange Dual Problem"
date:       2024-05-01 15:52:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
    - 优化理论
    - 拉格朗日对偶
---

# Introduction

The Lagrange dual problem is a fundamental concept in optimization theory that provides a powerful framework for solving constrained optimization problems. By introducing Lagrange multipliers, we can transform a constrained problem into an unconstrained one, often making it easier to solve and providing valuable insights into the original problem.

# Primal Problem

Consider a constrained optimization problem (the **primal problem**):

$$
\begin{align}
p^* = \min_{x \in \mathbb{R}^n} \quad & f(x) \\
\text{subject to} \quad & g_i(x) \leq 0, \quad i = 1, 2, \ldots, m
\end{align}
$$

where:
- $f(x)$ is the objective function
- $g_i(x) \leq 0$ are the inequality constraints
- $x \in \mathbb{R}^n$ is the decision variable
- $p^*$ is the optimal value of the primal problem

# Lagrange Function

The **Lagrange function** (or Lagrangian) is defined as:

$$
\mathcal{L}(x, \lambda) = f(x) + \sum_{i=1}^{m} \lambda_i g_i(x) = f(x) + \lambda^T g(x)
$$

where:
- $\lambda = [\lambda_1, \lambda_2, \ldots, \lambda_m]^T$ are the **Lagrange multipliers**
- $\lambda_i \geq 0$ for all $i$ (non-negativity constraint)
- $g(x) = [g_1(x), g_2(x), \ldots, g_m(x)]^T$ is the constraint vector

# Key Properties

## Property 1: Lower Bound

For every feasible $x$ (i.e., $x$ satisfying $g_i(x) \leq 0$ for all $i$) and every $\lambda \geq 0$, the objective function $f(x)$ is bounded below by the Lagrangian:

$$
f(x) \geq \mathcal{L}(x, \lambda)
$$

**Proof**: Since $g_i(x) \leq 0$ and $\lambda_i \geq 0$, we have $\lambda_i g_i(x) \leq 0$ for all $i$. Therefore:
$$
\mathcal{L}(x, \lambda) = f(x) + \sum_{i=1}^{m} \lambda_i g_i(x) \leq f(x)
$$

## Property 2: Primal Problem Reformulation

The primal problem can be reformulated using the Lagrangian as:

$$
p^* = \min_{x} \max_{\lambda \geq 0} \mathcal{L}(x, \lambda)
$$

This formulation shows that we first maximize the Lagrangian with respect to $\lambda$ (for fixed $x$), then minimize the result with respect to $x$.

# Lagrange Dual Function

The **Lagrange dual function** is defined as:

$$
G(\lambda) := \min_{x} \mathcal{L}(x, \lambda)
$$

**Key observations**:
- $G(\lambda)$ is always a lower bound on the optimal value $p^*$ for any $\lambda \geq 0$
- $G(\lambda)$ is concave (even if the original problem is not convex)
- The domain of $G(\lambda)$ is $\{\lambda \geq 0 : G(\lambda) > -\infty\}$

# Lagrange Dual Problem

The **Lagrange dual problem** is defined as:

$$
\begin{align}
d^* = \max_{\lambda} \quad & G(\lambda) \\
\text{subject to} \quad & \lambda \geq 0
\end{align}
$$

where $d^*$ is the optimal value of the dual problem.

# Duality Theory

## Weak Duality

**Theorem 1 (Weak Duality)**: For any optimization problem (convex or non-convex), weak duality holds:

$$
p^* \geq d^*
$$

**Proof**: For any feasible $x$ and any $\lambda \geq 0$:
$$
f(x) \geq \mathcal{L}(x, \lambda) \geq \min_{x'} \mathcal{L}(x', \lambda) = G(\lambda)
$$

Taking the minimum over all feasible $x$ on the left and the maximum over all $\lambda \geq 0$ on the right gives the result.

## Strong Duality

**Theorem 2 (Strong Duality)**: Under certain conditions (e.g., Slater's condition for convex problems), strong duality holds:

$$
p^* = d^*
$$

When strong duality holds, solving the dual problem is equivalent to solving the primal problem.

# Example

Consider the simple optimization problem:

$$
\begin{align}
\min_{x} \quad & x^2 \\
\text{subject to} \quad & x \geq 1
\end{align}
$$

**Solution**:
- Primal optimal value: $p^* = 1$ (achieved at $x = 1$)
- Lagrangian: $\mathcal{L}(x, \lambda) = x^2 + \lambda(1 - x)$
- Dual function: $G(\lambda) = \min_{x} [x^2 + \lambda(1 - x)] = \lambda - \frac{\lambda^2}{4}$
- Dual optimal value: $d^* = 1$ (achieved at $\lambda = 2$)

This example demonstrates strong duality: $p^* = d^* = 1$.

# Applications

The Lagrange dual problem has numerous applications in:
- **Machine Learning**: Support Vector Machines, regularization
- **Signal Processing**: Compressed sensing, sparse recovery
- **Economics**: Utility maximization, resource allocation
- **Engineering**: Optimal control, structural optimization

# References

1. [Duality (optimization) - Wikipedia](https://en.wikipedia.org/wiki/Duality_(optimization))
2. [EE227A Lecture 7: Duality - UC Berkeley](https://people.eecs.berkeley.edu/~elghaoui/Teaching/EE227A/lecture7.pdf)
3. [ELEC5470: Lagrange Duality - HKUST](https://palomar.home.ece.ust.hk/ELEC5470_lectures/slides_Lagrange_duality.pdf)
4. Boyd, S., & Vandenberghe, L. (2004). *Convex Optimization*. Cambridge University Press.
5. Bertsekas, D. P. (1999). *Nonlinear Programming*. Athena Scientific.