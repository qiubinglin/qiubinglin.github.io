---
layout:     post
title:      "Dual Space and Dual Map"
date:       2024-05-06 15:25:00
author:     "Bing"
catalog:    true
tags:
    - 线性代数
---

# Linear map
Let $V$ and $W$ be vector spaces over the same field $R$. A function $f: V \to W$ is a linear map when it satisfies
$$
    f(x + y) = f(x) + f(y)
    \\
    f(\alpha x) = \alpha f(x)
$$
for all $\alpha \in R$, $x,y \in V$.

# Linear form(Linear functional)
A linear form is a linear map from a vector space to its field of scalars.

# Dual space
Let $V$ be a vector space over field $K$, then the dual space of $V$, denoted  $V'$, is the vector space of all linear functionals on $V$. In other words,
$$
    V' = \mathcal{L}(V, R)
$$

# Dual basis
If $v_1,...,v_n$ is a basis of $V$, then the dual basis of $v_1,...,v_n$ is $\varphi_1,...,\varphi_n \in V'$ that satisfy
$$
    \varphi_j(v_k) = \begin{cases}
        1 \quad j = k
        \\
        0 \quad j \neq k
    \end{cases}
$$

# Dual map
If $T \in \mathcal{L}(V, W)$, then the dual map of $T$ is the linear map $T' \in \mathcal{L}(V', W')$.

# References
Linear Algebra Done Right. pp.101-104

[https://en.wikipedia.org/wiki/Dual_space](https://en.wikipedia.org/wiki/Dual_space)

[https://www.zhihu.com/question/38464481](https://www.zhihu.com/question/38464481)