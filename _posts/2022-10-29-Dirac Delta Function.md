---
layout:     post
title:      "狄拉克δ函数"
date:       2022-10-29 16:38:00
author:     "Bing"
catalog:    true
tags:
    - δ函数
    - 广义函数
---

# 定义
$\delta(x)$ 是广义函数，它被表述为
$$
    \delta(x) = 
    \begin{cases}
    \infin, x = 0 \\
    0, x \neq 0
    \end{cases}
$$
并且有以下积分性质
$$
    \int_{-\infin}^{\infin} f(x) \delta(x) dx = f(0)
$$

我们可以用函数序列的方式表示（如正态分布序列的极限）
$$
    \delta(x) = \lim_{b->0} \frac{1}{|b|\sqrt{\pi}} e^{(-x/b)^2}
$$

# 性质
## 缩放
$$
    \int_{-\infin}^{\infin} \delta(\alpha x) dx = \int_{-\infin}^{\infin} \delta(u) \frac{du}{|\alpha|} = \frac{1}{|\alpha|}
$$

## 代数性质
$$
    x \delta(x) = 0
$$
如果 $xf(x) = xg(x)$，那么
$$
    f(x) = g(x) + c\delta(x)
$$
$c$ 是一个常数。

## 采样
$$
    \int_{-\infin}^{\infin} f(t) \delta(t-T) dt = f(T)
$$

## 复合函数
**这是理解 $\delta$ 函数的关键**。

设 $g(x)$ 是连续可导函数且 $g'(x) \neq 0, \forall x \in R$，则
$$
    \int_R \delta(g(x)) f(g(x)) |g'(x)| dx = \int_{g(R)} \delta(u)f(u)du
$$
进而
$$
    \delta(g(x)) = \sum_i \frac{\delta(x - x_i)}{|g'(x_i)|}
$$
其中 $x_i$ 是 $g(x)$ 的实根。