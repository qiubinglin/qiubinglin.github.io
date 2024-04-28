---
layout:     post
title:      "Newton-Raphson Method"
date:       2024-04-28 13:18:00
author:     "Bing"
catalog:    true
tags:
    - 凸优化
---

# Newton-Raphson Method
Given a twice differentiable function $f: R \to R$, we seek to solve the optimization problem
$$
    minimize \; f(x), \quad x \in R
$$

Consider the second Taylor expansion of $f$ around $x_k$, which is
$$
    f(x_k + t) \approx f(x_k) + f'(x_k)(t - x_k) + \frac{1}{2}f''(x_k)(t - x_k)^2
$$

Setting the next iterate $x_{k+1} = x_k + t$, if the second derivative is positive, the quadratic approximation is a convex function of $t$, and its minimum can be found by setting the derivative to zero. Since
$$
    f'(x_k) + f''(x_k) t = 0
$$
the minimum is achieved for
$$
    t = - \frac{f'(x_k)}{f''(x_k)}
$$

That is, Newton-Raphson method attempts to solve this problem by constructing a sequence $\{x_k\}$ from an initial guess $x_0$ that converges towards a minimizer $x_{*}$ of $f$ by using the method above.

# Higher dimension
The second Taylor expansion
$$
    f(x_k + t) \approx f(x_k) + \triangledown f(x_k) (t - x_k) + \triangledown^2 f(x_k) (t - x_k)^2
$$
the minimum is achieved for
$$
    t = -[f''(x_k)]^{-1} f'(x_k)
$$
$$
    x_{k+1} = x_k - [f''(x_k)]^{-1} f'(x_k)
$$

# References
[https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization](https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization)