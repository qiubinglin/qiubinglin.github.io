---
layout:     post
title:      "Quadprog Programming"
date:       2024-03-30 08:47:00
author:     "Bing"
catalog:    true
tags:
    - 应用数学
---

# Definition
The quadprog qrogramming problem with $n$ variables and $m$ constraints can be formulated follows. Given:
1. a real-valued, $n$-dimensional vector $c$,
2. an $n \times n$ real symmetric matrix $H$,
3. an $m \times n$ real metrix $A$,
4. an $m$-dimensional real vector $b$.

The objective of quadprog qrogramming is to find an $n$-dimensional vector $x$, that will

$$
   minimize \quad \frac{1}{2} x^T H x + c^T x
$$
$$
    subject \; to \quad Ax \leq b
$$

# Constrained linear least square problem
Transform the square fomulatoin as follow:
$$
    ||Cx - d||_2^2 = (Cx - d)^T(Cx - d) \\
    = (x^T C^T - d^T)(Cx - d) \\
    = (x^T C^T Cx) - (x^T C^T d - d^T Cx) + d^Td \\
    = \frac{1}{2} x^T (2C^T C) x + (-2C^T d)^T x + d^T d
$$

Let $H = 2C^T C$ and $c = -2C^T d$, then we get the quadprog fomulation.

# Active set method

# Interior point method

# References
Wiki: [https://en.wikipedia.org/wiki/Quadratic_programming](https://en.wikipedia.org/wiki/Quadratic_programming)

Matlab: [https://ww2.mathworks.cn/help/optim/ug/least-squares-model-fitting-algorithms.html#buc5ri4](https://ww2.mathworks.cn/help/optim/ug/least-squares-model-fitting-algorithms.html#buc5ri4)

Active set method: 

[https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail](https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail)

[https://arxiv.org/pdf/2103.16236.pdf](https://arxiv.org/pdf/2103.16236.pdf)

Interior point method: [https://www.maths.ed.ac.uk/hall/NATCOR_2016/IPMsQP.pdf](https://www.maths.ed.ac.uk/hall/NATCOR_2016/IPMsQP.pdf)