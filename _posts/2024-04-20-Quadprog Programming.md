---
layout:     post
title:      "Quadratic Programming: Theory and Applications"
date:       2024-04-20 16:42:00
author:     "Bing"
catalog:    true
tags:
    - 应用数学
    - 优化理论
    - 二次规划
---

## Introduction

Quadratic Programming (QP) is a fundamental optimization problem that finds applications in various fields including finance, machine learning, control theory, and operations research. It involves minimizing a quadratic objective function subject to linear constraints.

## Problem Formulation

The standard quadratic programming problem with $n$ variables and $m$ constraints can be formulated as follows:

**Given:**
- A real-valued, $n$-dimensional vector $c \in \mathbb{R}^n$
- An $n \times n$ real symmetric matrix $H \in \mathbb{R}^{n \times n}$
- An $m \times n$ real matrix $A \in \mathbb{R}^{m \times n}$
- An $m$-dimensional real vector $b \in \mathbb{R}^m$

**Objective:** Find an $n$-dimensional vector $x \in \mathbb{R}^n$ that minimizes:

$$\min_{x} \quad \frac{1}{2} x^T H x + c^T x$$

**Subject to:**
$$Ax \leq b$$

## Mathematical Properties

### Objective Function
The objective function $f(x) = \frac{1}{2} x^T H x + c^T x$ consists of:
- **Quadratic term**: $\frac{1}{2} x^T H x$ (where $H$ is the Hessian matrix)
- **Linear term**: $c^T x$

### Hessian Matrix Properties
- If $H$ is **positive definite**, the problem has a unique global minimum
- If $H$ is **positive semidefinite**, the problem may have multiple minima
- If $H$ is **indefinite**, the problem may be unbounded

## Special Cases

### 1. Constrained Linear Least Squares Problem

A common special case is the constrained linear least squares problem:

$$\min_{x} \quad \|Cx - d\|_2^2 \quad \text{subject to} \quad Ax \leq b$$

**Transformation to QP format:**

$$\begin{align}
\|Cx - d\|_2^2 &= (Cx - d)^T(Cx - d) \\
&= (x^T C^T - d^T)(Cx - d) \\
&= x^T C^T Cx - x^T C^T d - d^T Cx + d^T d \\
&= x^T C^T Cx - 2d^T Cx + d^T d \\
&= \frac{1}{2} x^T (2C^T C) x + (-2C^T d)^T x + d^T d
\end{align}$$

**Note:** The constant term $d^T d$ can be omitted from the optimization since it doesn't affect the optimal solution.

By setting $H = 2C^T C$ and $c = -2C^T d$, we obtain the standard QP formulation.

### 2. Portfolio Optimization
In finance, QP is used for portfolio optimization:
$$\min_{w} \quad \frac{1}{2} w^T \Sigma w \quad \text{subject to} \quad \mu^T w \geq R, \quad \sum_i w_i = 1$$
where $w$ are portfolio weights, $\Sigma$ is the covariance matrix, and $\mu$ are expected returns.

## Solution Methods

### 1. Active Set Method
- **Principle**: Iteratively identifies which constraints are active (binding) at the solution
- **Advantages**: Efficient for problems with few active constraints
- **Complexity**: $O(n^3)$ per iteration
- **Best for**: Small to medium-sized problems

### 2. Interior Point Method
- **Principle**: Approaches the solution from the interior of the feasible region
- **Advantages**: Polynomial complexity, handles large problems well
- **Complexity**: $O(\sqrt{n} \log(1/\epsilon))$ iterations
- **Best for**: Large-scale problems

### 3. Sequential Quadratic Programming (SQP)
- **Principle**: Solves a sequence of QP subproblems
- **Advantages**: Handles nonlinear constraints
- **Best for**: General nonlinear optimization problems

## Optimality Conditions

### KKT Conditions
For the QP problem, the Karush-Kuhn-Tucker (KKT) conditions are:

$$\begin{align}
Hx + c + A^T \lambda &= 0 \quad \text{(Stationarity)} \\
Ax - b &\leq 0 \quad \text{(Primal feasibility)} \\
\lambda &\geq 0 \quad \text{(Dual feasibility)} \\
\lambda_i(Ax - b)_i &= 0 \quad \text{(Complementary slackness)}
\end{align}$$

where $\lambda$ is the vector of Lagrange multipliers.

## Implementation Considerations

### Numerical Stability
- Ensure $H$ is well-conditioned
- Use appropriate scaling for variables and constraints
- Consider regularization techniques for ill-conditioned problems

### Software Tools
- **MATLAB**: `quadprog` function
- **Python**: `cvxopt`, `scipy.optimize`
- **R**: `quadprog` package
- **Julia**: `OSQP`, `COSMO`

## Applications

1. **Finance**: Portfolio optimization, risk management
2. **Machine Learning**: Support Vector Machines, kernel methods
3. **Control Theory**: Model Predictive Control, optimal control
4. **Operations Research**: Resource allocation, scheduling
5. **Signal Processing**: Filter design, beamforming

## Conclusion

Quadratic programming provides a powerful framework for solving optimization problems with quadratic objectives and linear constraints. Understanding the mathematical foundations and solution methods is crucial for effective implementation in real-world applications.

## References

### General Resources
- [Quadratic Programming - Wikipedia](https://en.wikipedia.org/wiki/Quadratic_programming)
- [MATLAB Optimization Toolbox](https://ww2.mathworks.cn/help/optim/ug/least-squares-model-fitting-algorithms.html#buc5ri4)

### Active Set Method
- [Goldfarb-Idnani Method](https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail)
- [Modern Active Set Methods](https://arxiv.org/pdf/2103.16236.pdf)
- [Active Set Methods for QP](https://escholarship.org/content/qt2sp3173p/qt2sp3173p.pdf?t=ml512r)

### Interior Point Method
- [Interior Point Methods for QP](https://www.maths.ed.ac.uk/hall/NATCOR_2016/IPMsQP.pdf)

### Mathematical Foundations
- [Moore–Penrose Inverse](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse)
- [Definite Matrix](https://en.wikipedia.org/wiki/Definite_matrix)
- [Hessian Matrix](https://en.wikipedia.org/wiki/Hessian_matrix)
- [Hessian Matrix Properties](https://math.okstate.edu/people/lebl/osu4013-s17/hessian.pdf)
- [Newton–Raphson Method](https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization)
- [KKT Conditions](https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions)
- [Saddle Point](https://en.wikipedia.org/wiki/Saddle_point)