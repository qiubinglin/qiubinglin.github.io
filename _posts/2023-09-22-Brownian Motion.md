---
layout:     post
title:      "布朗运动"
date:       2023-09-22 17:42:00
author:     "Bing"
catalog:    true
tags:
    - 随机过程
---

# 布朗运动(Brown Motion)
布朗运动在数学上被称为维纳过程(Wiener Process)，它具有如下性质
1. $B_0 = 0$
2. $B_t$ 是连续的
3. 独立增量性，对于不重叠区间 $[s, t]$，随机变量 $B_t - B_s$ 之间是相互独立的，即布朗运动是马尔可夫过程
4. 平稳性，且 $B_t - B_s \sim N(0, t - s)$ 对于 $0 \leq s < t$

$N(\mu, \sigma^2)$ 是期望为 $\mu$，方差为 $\sigma^2$ 的标准正态分布。

## 布朗运动的二次变差(Quadratic Variation)
布朗运动在区间 $[0, T]$ 连续但却处处不可微，它的二次变差
$$
    [B]_t = \sum_k (B_{t_{k}} - B_{t_{k-1}})^2 = T
$$
微分形式则为
$$
    (dB_t)^2 = dt
$$

### 证明
考虑一个均匀划分 $||D|| = [\frac{(k-1)T}{n}, \frac{kT}{n}]_k$，我们要证明
$$
    n \to \infty \Rightarrow P([B]_t \to T) = 1
$$

令 $X = B_{t_{k}} - B_{t_{k-1}}$，那么 $X \sim N(0, \frac{T}{n})$

先计算 $[B]_t$ 的期望
$$
    E(X^2) = Var(X) = \frac{T}{n}
    \\
    E([B]_t) = \sum_k E(X_k^2) = T
$$

再计算 $[B]_t$ 的方差，因为 $X_k$ 是独立增量
$$
    Var([B]_t) = \sum_k Var(X_k^2)
$$

注意，若 $X \sim N(0, \sigma^2)$，所以 $X^2 \sim \sigma^2 \cdot \chi^2(1)$，所以
$$
    Var(X^2) = 2 \sigma^4
    \\
    Var([B]_t) = 2n \cdot (\frac{T}{n})^2 = \frac{2T^2}{n}
$$

应用切比雪夫不等式
$$
    P(|[B]_t - T| \ge \epsilon) \le \frac{Var([B]_t)}{\epsilon^2} = \frac{2T^2}{n \epsilon^2}
$$
右边随着 $n \to \infty$ 趋于 $0$。

## 几何布朗运动(Geometric Brownian motion)
几何布朗运动（Geometric Brownian Motion, GBM）是金融中最常用于建模股票价格的随机过程。

***定义*** 随机过程 $S_t$ 是几何布朗运动(GBM)，当它满足以下随机微分方程
$$
    dS_t = \mu S_t dt + \sigma S_t dB_t
$$
其中
* $dS_t$ 是资产价格
* $\mu$ 是漂移率常数，代表平均收益率（价格的确定性增长部分）
* $\sigma$ 是波动率常数，控制价格“抖动”的程度
* $B_t$ 是布朗运动

资产价格的相对变动
$$
    \frac{dS_t}{S_t} = \mu dt + \sigma dB_t
$$
令 $X = \frac{dS_t}{S_t}$，$X \sim N(\mu, \sigma^2 dt)$

# Appendix
## 马尔可夫过程(Markov Process)
假设随机过程 $[X_1, X_2,...]$ 有马尔可夫性质，下一个随机变量的分布仅依赖于当前随机变量，即
$$
    Pr(X_{n+1} | X_1 = x_1, X_2 = x_2..., X_n = x_n) = Pr(X_{n+1} | X_n = x_n)
$$
那么该随机过程为马尔可夫过程。

## Second Variation
在变分法中，目标是寻找泛函 $J[y]$ 的极值（如最速降线、最小曲面问题）。通过令泛函的一次变分（First Variation）$\delta J$ 为零，得到欧拉-拉格朗日方程，从而找到可能的极值函数（驻点）。但一次变分无法判断该极值是极小值、极大值还是鞍点，这时需要引入二次变分。

### Definition
二次变分是泛函 $J[y]$ 在极值函数附近的二阶展开项，类似于多元函数泰勒展开中的二阶导数。形式上：
$$
    \Delta J = J[y + \epsilon] - j[y] = \delta J + \frac{1}{2} \delta^2 J + ...
$$
其中 $\delta^2 J$ 即是二次变分。

## 中值定理
***定义1*** 设 $f$ 是定义在度量空间 $X$ 的实值函数，称 $f$ 在 $p \in X$ 取得局部最大值，如果存在 $\delta > 0$，当 $d(p, q) < \delta$ 且 $q \in X$ 时有 $f(p) \ge f(q)$。

***定理1*** 设 $f$ 定义在 $[a,b]$ 上，若 $x \in [a,b]$ 且 $f(x)$ 是局部最大值且 $f'(x)$ 存在，那么 $f'(x) = 0$。

**证明**

根据定义1:
$$
    a < x - \delta < x < x + \delta < b
$$
若 $x - \delta < t < x$,
$$
    \lim_{t->x} \frac{f(t) - (x)}{t - x} = f'(x)
$$
那么 $f'(x) \ge 0$。对应的若 $x < t < x + \delta$, 那么 $f'(x) \le 0$。

因此 $f'(x) = 0$。

***一般中值定理*** 设 $f,g$ 是 $[a,b]$ 上的连续实函数，它们在 $(a,b)$ 中可微，那么便有一点 $x \in (a,b)$ 使得
$$
    [f(b) - f(a)]g'(x) = [g(b) - g(a)]f'(x)
$$
**证明** 令 $h(t) = [f(b) - f(b)]g(t) - [g(b) - g(a)]f(t)$，则有
$h(a) = h(b)$，易论证存在 $x \in (a, b)$ 使得 $h(x)$ 取极值，即 $h'(x)=0$。

***中值定理（特例）*** 设 $f$ 是 $[a,b]$ 上的连续实函数，它在 $(a,b)$ 中可微，那么便有一点 $x \in (a,b)$ 使得
$$
    f(b) - f(a) = (b - a)f'(x)
$$

## Quadratic Variation
描述随机过程路径的“粗糙度”或累积波动。对于随机过程 $X_t$，其二次变差定义为
$$
    [X]_t = \lim_{||D||->0} \sum (X_{t_i} - X_{t_{i-1}})^2
$$
其中 $||D||$ 是区间 $[0,T]$ 的一个划分。

若 $X(t)$ 是一个连续且在 $[0, T]$ 处处可微的函数，根据中值定理得到如下不等式
$$
    \sum (X_{t_i} - X_{t_{i-1}})^2 = \sum(t_i - t_{i-1})^2 f'(s_{i-1})^2
    \\
    \le max_{s\in(0,T)}f(s)^2 \cdot \sum(t_i - t_{i-1})^2
    \\
    \le max_{s\in(0,T)}f(s)^2 \cdot max(t_i - t_{i-1}) \cdot T
$$
随着 $||D||$ 的不断细分，$X(t)$ 的二次变差趋于0。

## 随机游走(Random Walk)
在足够的时间尺度下，随机游走近似于布朗运动。

## 正态分布与卡布分布

## 切比雪夫不等式

# References
李育强 姚强. 应用随机过程.

[https://en.wikipedia.org/wiki/Markov_chain](https://en.wikipedia.org/wiki/Markov_chain)

[https://en.wikipedia.org/wiki/Wiener_process](https://en.wikipedia.org/wiki/Wiener_process)

[https://en.wikipedia.org/wiki/Geometric_Brownian_motion](https://en.wikipedia.org/wiki/Geometric_Brownian_motion)

[https://zhuanlan.zhihu.com/p/38293827](https://zhuanlan.zhihu.com/p/38293827)