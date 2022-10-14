---
layout:     post
title:      "插值"
subtitle:   " \"关于插值的一点介绍\""
date:       2022-10-09 17:15:00
author:     "Bing"
catalog: true
tags:
    - 数值计算
    - 插值
---

# 插值的定义
插值，即使用插值函数去近似真实函数。多项式函数非常适用于计算机计算，因此插值函数通常选用多项式函数。其严格定义如下。

如果对于每一个 $1 \leq i \leq n$，$y_i = P(x_i)$，则称函数 $y = P(x)$ 插值数据点 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$。

# 拉格朗日插值
假设给定 $n$ 个数据点 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$，则
$$
    y = \sum_{i=1}^n { y_i \prod_{j=1,j \neq i}^n \frac{x - x_j}{x_i - x_j} }
$$
是这 $n$ 个点的拉格朗日插值多项式。

# 多项式插值主定理
令 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$ 是平面中的 $n$ 个点，具有不同的 $x_i$ 坐标，则存在一个且仅有一个 $n-1$ 次或者更低次的多项式 $P$ 满足 $y_i = P(x_i), i=1,2...n$。

证明。拉格朗日插值证明 $P$ 的存在性，代数基本定理结合反证法证明 $P$ 的唯一性。

# 牛顿差商
用 $f[x_1...x_n]$ 表示（唯一）多项式的 $x^{n-1}$ 项的系数，该多项式插值 $((x_1, f(x_1))... (x_n, f(x_n)))$。

牛顿差商公式
$$
    P(x) = f[x_1] + f[x_1, x_2](x - x_1) +...+ f[x_1...x_n](x - x_1)...(x - x_{n-1})
$$
通过递归带入 $x_1...x_k$ 可以计算出 $f[x_1...x_k]$。
$$
    f[x_1] = f(x_1)
$$
$$
    f[x_1...x_k] = \frac{f[x_2...x_k] - f[x_1...x_{k-1}]}{x_k - x_1}, (k > 1)
$$

# 插值误差
如果 $P(x)$ 是 $n - 1$ 阶或更低阶的插值多项式，拟合数据点 $(x_1, y_1)...(x_n, y_n)$。那么 $P(x)$ 的插值误差是
$$
    f(x) - P(x) = \frac{f^{(n)}(c)}{n!}(x - x_1)...(x - x_n)
$$
其中 $c$ 在最小和最大的 $n+1$ 个数字 $x, x_1...x_n$ 之间。

证明

$P_{n-1}(t)$ 是数据点 $(x_1, y_1)...(x_n, y_n)$ 的插值多项式，若新加入任意点 $(x, y)$，则
$$
    P_{n}(t) = P_{n-1}(t) + f[x_1...x_n, x](t - x_1)...(t - x_n)
$$
于是对于任意点 $x$ 有
$$
    f(x) = P_{n}(x) = P_{n-1}(x) + f[x_1...x_n, x](x - x_1)...(x - x_n)
$$
现在定义
$$
    h(t) = f(t) - P_{n-1}(t) - f[x_1...x_n, x](t - x_1)...(t - x_n)
$$
因为 $h(x) = h(x_1) =...= h(x_n) = 0$，根据罗尔定理函数 $h$ 在最小和最大的 $n+1$ 个数字 $x, x_1...x_n$ 之间存在 $n$ 个点满足 $h'=0$，以此类推此区间存在一个点 $c$ 满足
$$
h^{(n)}(c) = 0
$$
又因为
$$
    h^{(n)}(t) = f^{(n)}(t) - f[x_1...x_n, x](n!)
$$
则
$$
    f[x_1...x_n, x] = \frac{f^{(n)}(c)}{n!}
$$

# 龙格现象
在插值均匀分布的点集时，多项式在插值区间的端点附近扭动。因此，数据点选取对插值误差有很大的影响。

# 附录
## 代数基本定理
每个复系数 $n$ 次多项式 $p(x) = a_0 + a_1x +...+a_nx^n (a_n \neq 0)$ 有乘积表达式
$$
    p(x) = a_n(x - x_1)(x - x_2)...(x - x_n)
$$
其中复数 $x_1...x_n$ 除顺序外是唯一确定的。

## 罗尔定理
如果函数 $f$ 在 $[a, b]$ 上连续，$(a, b)$ 上可导，且 $f(a) = f(b)$，那么 $(a, b)$ 上存在一点 $\xi(a < \xi < b)$ 使得 $f'(\xi) = 0$。