---
layout:     post
title:      "ENO and WENO Schemes"
date:       2023-03-19 10:57:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
---

ENO的思想就是用多项式插值去近似函数，进而近似函数的导数。为方便讨论，给定等间距格点。
$$
    ... < x_0 < x_1 ... < x_n < ...
$$
$$
    x_k - x_{k-1} = \Delta x
$$

***定义1***
$I_i = (x_{i-1/2}, x_{i+1/2})$ 为一个计算格点。

***定义2***
$\overline{u}_i = \frac{1}{\Delta x} \int_{x_{i-1/2}}^{x_{i+1/2}} u(x) dx$，为关于一个计算格点 $I_i$ 的均值。

***定义3***
$$
    U(x) = \int_{x_a}^x u(\xi) d\xi
$$
其中 $x_a$ 是任意给定定义域内的值。

# Reconstruction
对于给定区间 $S= \{I_{i-2}, I_{i-1}, I_{i}\}$，根据Lagrange插值可以构建插值多项式 $P(x)$，有
$$
    U(x) \approx P(x)
$$
进一步地
$$
    u(x) \approx P'(x)
$$
于是可以整理出
$$
    u_{i+1/2}^{(1)} = \frac{1}{3} \overline{u}_{i-2} - \frac{7}{6} \overline{u}_{i-1} + \frac{11}{6} \overline{u}_{i}
$$

不同的区间选择会有不同的近似。

对于 $S= \{I_{i-1}, I_{i}, I_{i+1}\}$ 有
$$
    u_{i+1/2}^{(2)} = -\frac{1}{6} \overline{u}_{i-1} + \frac{5}{6} \overline{u}_{i} + \frac{1}{3} \overline{u}_{i+1}
$$

对于 $S= \{I_{i-2}, I_{i-1}, I_{i}\}$ 有
$$
    u_{i+1/2}^{(3)} = \frac{1}{3} \overline{u}_{i} + \frac{5}{6} \overline{u}_{i+1} - \frac{1}{6} \overline{u}_{i+2}
$$

# ENO Approximation

# WENO Approximation