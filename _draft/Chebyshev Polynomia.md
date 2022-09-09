---
layout:     post
title:      "切比雪夫多项式"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog: true
tags:
    - 数值计算
    - 插值
    - 多项式
    - 切比雪夫
---
# 预备知识
1、代数基本定理。2、余弦求和公式。

## 余弦求和公式
$$
    cos(x \pm y) = cosx cosy \mp sinx siny
$$

# 切比雪夫多项式
定义 $n$ 阶切比雪夫多项式
$$
T_n(x) = cos(n \ arccosx), \ x \in [-1, 1]
$$
一般的，令 $cosy = x$，
$$
    T_{n-1}(x) = cos((n-1)y) = cos(ny)cosy + sin(ny)siny
$$
$$
    T_{n+1}(x) = cos((n+1)y) = cos(ny)cosy - sin(ny)siny
$$
$$
    T_{n-1}(x) + T_{n+1}(x) = 2cos(ny)cosy = 2xT_{n}(x)
$$
得到递归关系
$$
    T_{n+1}(x) = 2xT_{n}(x) - T_{n-1}(x)
$$

$T_n(x)$ 为关于 $x$ 的多项式。由 $T_1 = x, \ T_2 = 2x^2-1$ 以及递归关系可知。

$deg(T_n)=n$ 且主导系数是 $2^{n-1}$。

$T_n(x)$ 的零点是
$$
    ny = \frac{odd \cdot \pi}{2}, \ y \in [0, \pi]
$$
$$
    x_i = cos \frac{(2i - 1)\pi}{2n}, \ i = 1...n
$$

## 切比雪夫插值点集定理
选择 $x_1...x_n \in [-1, 1]$，使得
$$
    f_n = max_{x \in [-1, 1]}|\prod_{i=1}^n (x - x_i)|
$$
最小。则
$$
    x_i = cos \frac{(2i - 1)\pi}{2n}, \ i = 1...n
$$
$f_n$ 的最小值是 $\frac{1}{2^{n-1}}$。$x_i$ 的取值也可由如下方式得到
$$
    \prod_{i=1}^n (x - x_i) = \frac{1}{2^{n-1}} T_n(x)
$$
其中 $T_n$ 为 $n$ 阶切比雪夫多项式。

证明。令 $P_n = \prod_{i=1}^n (x - x_i)$，假设存在 $x_1...x_n \in [-1, 1]$ 使得 $|P_n| < \frac{1}{2^{n-1}}$，那么 $t_n = P_n - \frac{1}{2^{n-1}} T_n(x)$ 在正负间往返 $n+1$ 次，这是因为 $T_n$ 在 $-1$ 和 $1$ 间往返 $n+1$ 次，可知 $t_n$ 有 $n$ 个零点。又因为 $P_n$ 和 $\frac{1}{2^{n-1}} T_n(x)$ 均为首一多项式，所以 $t_n$ 是 $n-1$ 阶多项式，至多有 $n-1$ 个零点，因此假设不成立。