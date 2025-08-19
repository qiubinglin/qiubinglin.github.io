---
layout:     post
title:      "Lagrange Multiplier and KKT Conditions"
date:       2024-04-30 17:38:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
    - 数学优化
    - 拉格朗日乘数
---

# Lagrange Multiplier

The basic idea of the Lagrange multiplier method is to convert a constrained optimization problem into a form such that the derivative test of an unconstrained problem can still be applied.

## Problem Formulation

Consider the following equality-constrained optimization problem:

$$
\begin{align}
\min_{x \in \mathbb{R}^n} \quad & f(x) \\
\text{subject to} \quad & g_i(x) = 0, \quad i = 1, 2, \ldots, m
\end{align}
$$

where:
- $f(x)$ is the objective function to be minimized
- $g_i(x) = 0$ are the equality constraints
- $x \in \mathbb{R}^n$ is the decision variable vector

## Lagrange Function

The Lagrange function (or Lagrangian) is defined as:

$$
\mathcal{L}(x, \lambda) = f(x) + \sum_{i=1}^{m} \lambda_i g_i(x) = f(x) + \lambda^T g(x)
$$

where:
- $\lambda = [\lambda_1, \lambda_2, \ldots, \lambda_m]^T$ are the Lagrange multipliers
- $g(x) = [g_1(x), g_2(x), \ldots, g_m(x)]^T$ is the constraint vector

## First-Order Necessary Conditions

The optimal solution $(x^*, \lambda^*)$ must satisfy the following first-order necessary conditions:

$$
\begin{align}
\nabla_x \mathcal{L}(x^*, \lambda^*) &= \nabla f(x^*) + \sum_{i=1}^{m} \lambda_i^* \nabla g_i(x^*) = 0 \\
g_i(x^*) &= 0, \quad i = 1, 2, \ldots, m
\end{align}
$$

These conditions can be written more compactly as:

$$
\begin{align}
\nabla_x \mathcal{L}(x^*, \lambda^*) &= 0 \\
g(x^*) &= 0
\end{align}
$$

## Geometric Interpretation

The Lagrange multiplier method has an elegant geometric interpretation: at the optimal point, the gradient of the objective function $\nabla f(x^*)$ must be a linear combination of the gradients of the constraint functions $\nabla g_i(x^*)$. This means that the objective function's gradient is orthogonal to the tangent space of the constraint surface.

# Karush-Kuhn-Tucker (KKT) Conditions

The KKT conditions extend the Lagrange multiplier method to handle both equality and inequality constraints.

## Problem Formulation

Consider the following general optimization problem:

$$
\begin{align}
\min_{x \in \mathbb{R}^n} \quad & f(x) \\
\text{subject to} \quad & g_i(x) = 0, \quad i = 1, 2, \ldots, m \\
& h_j(x) \leq 0, \quad j = 1, 2, \ldots, p
\end{align}
$$

## Extended Lagrange Function

The extended Lagrange function is:

$$
\mathcal{L}(x, \lambda, \mu) = f(x) + \sum_{i=1}^{m} \lambda_i g_i(x) + \sum_{j=1}^{p} \mu_j h_j(x)
$$

where:
- $\lambda_i$ are Lagrange multipliers for equality constraints
- $\mu_j$ are Lagrange multipliers for inequality constraints (also called KKT multipliers)

## KKT Conditions

The KKT conditions are the first-order necessary conditions for optimality:

### 1. Stationarity
$$
\nabla_x \mathcal{L}(x^*, \lambda^*, \mu^*) = \nabla f(x^*) + \sum_{i=1}^{m} \lambda_i^* \nabla g_i(x^*) + \sum_{j=1}^{p} \mu_j^* \nabla h_j(x^*) = 0
$$

### 2. Primal Feasibility
$$
\begin{align}
g_i(x^*) &= 0, \quad i = 1, 2, \ldots, m \\
h_j(x^*) &\leq 0, \quad j = 1, 2, \ldots, p
\end{align}
$$

### 3. Dual Feasibility
$$
\mu_j^* \geq 0, \quad j = 1, 2, \ldots, p
$$

### 4. Complementary Slackness
$$
\mu_j^* h_j(x^*) = 0, \quad j = 1, 2, \ldots, p
$$

## Karush-Kuhn-Tucker Theorem

### Sufficiency Condition
**Theorem**: If $(x^*, \lambda^*, \mu^*)$ satisfies the KKT conditions and the following conditions hold:
- $f(x)$ is convex
- $g_i(x)$ are affine (linear) functions
- $h_j(x)$ are convex functions
- $\mu_j^* \geq 0$ for all $j$

Then $x^*$ is a global optimal solution.

### Necessity Condition
**Theorem**: Suppose that:
- $f(x)$ and $h_j(x)$ are continuously differentiable and convex
- $g_i(x)$ are continuously differentiable and affine
- There exists a point $\bar{x}$ such that $h_j(\bar{x}) < 0$ for all $j$ (Slater's condition)

Then, if $x^*$ is an optimal solution, there exist Lagrange multipliers $\lambda^*$ and $\mu^*$ such that $(x^*, \lambda^*, \mu^*)$ satisfies the KKT conditions.

## Example: Quadratic Programming

Consider the quadratic programming problem:

$$
\begin{align}
\min_{x \in \mathbb{R}^n} \quad & \frac{1}{2}x^T Q x + c^T x \\
\text{subject to} \quad & Ax = b \\
& x \geq 0
\end{align}
$$

The KKT conditions become:

$$
\begin{align}
Qx^* + c + A^T \lambda^* - \mu^* &= 0 \\
Ax^* &= b \\
x^* &\geq 0 \\
\mu^* &\geq 0 \\
\mu_i^* x_i^* &= 0, \quad \forall i
\end{align}
$$

## Applications

Lagrange multipliers and KKT conditions are fundamental in:
- **Economics**: Utility maximization, cost minimization
- **Engineering**: Structural optimization, control systems
- **Machine Learning**: Support Vector Machines, regularization
- **Finance**: Portfolio optimization, risk management
- **Operations Research**: Resource allocation, scheduling

# References

1. [Lagrange Multiplier - Wikipedia](https://en.wikipedia.org/wiki/Lagrange_multiplier)
2. [Karush–Kuhn–Tucker Conditions - Wikipedia](https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions)
3. Boyd, S., & Vandenberghe, L. (2004). *Convex Optimization*. Cambridge University Press.
4. Nocedal, J., & Wright, S. J. (2006). *Numerical Optimization*. Springer.