---
layout:     post
title:      "Monte Carlo Method"
date:       2023-07-07 17:33:00
author:     "Bing"
catalog:    true
tags:
    - 随机过程
---

Monte Carlo方法是一种以概率统计理论为指导的数值计算方法。

# Monte Carlo Type 1 Problem
Monte Carlo一型问题可以被认为是，用随机样本对函数求均值。

函数 $f(x)$ 在区间 $[a, b]$ 的均值是
$$
    \frac{1}{b - a} \int_{a}^{b} f(x) dx
$$
显然，若 $u_0...u_n$ 是对 $x$ 的随机采样，根据大数定律有
$$
    \lim_{n->\infty} \frac{1}{n} \sum_{i=0}^{n} f(u_i) = \frac{1}{b - a} \int_{a}^{b} f(x) dx
$$

# Monte Carlo Type 2 Problem
Monte Carlo二型问题和一型问题并没有严格的分界线，二型问题的一个典型例子是求解圆的面积。设想一个圆和以该圆为内切的正方形的区域，向该区域随机撒点，点在圆上取 $1$ 否则为 $0$，显然对该随机变量 $X$ 有
$$
    \lim_{n->\infty} \frac{1}{n} \sum_{i=0}^{n} X_i = \frac{Area(circle)}{Area(Rect)}
$$

# Type 1 or Type 2 Monte Carlo误差分析
设随机变量 $X_i$ 对应 $f$ 在随机点上的值。随机变量 $Y$
$$
    Y = \frac{X_1 + X_2 + ... + X_n}{n}
$$
$$
    E[\frac{X_1 + X_2 + ... + X_n}{n}] = n A/n = A
$$
则
$$
    Var(Y) = E[(\frac{X_1 + X_2 + ... + X_n}{n} - A)^2] = \frac{1}{n} \sum E[(X_i - A)^2] = \frac{1}{n^2} n \sigma^2 = \frac{\sigma^2}{n}
$$
对于1型和2型Monte Carlo问题，误差
$$
    Error \propto n^{-1/2}
$$

# References
Timothy Sauer. Numerical Analysis. Chapter 9.