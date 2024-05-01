---
layout:     post
title:      "随机变量及其分布"
date:       2023-09-20 16:03:00
author:     "Bing"
catalog:    true
tags:
    - 随机过程
---

# 概率空间(Probability Space)
概率空间的数学描述为 $(\Omega, \mathcal{F}, P)$，$\Omega$ 是样本空间，$\mathcal{F}$ 是事件空间，$P$ 是概率函数。

***定义*** 随机试验中基本事件的集合称为概率空间。

***定义*** 设 $\Omega$ 是一个概率空间，$F \subseteq \Omega$ 称为事件。

***定义*** 事件空间 $\mathcal{F}$ 到实数区间 $[0,1]$ 的映射 $P$ 称为概率函数。

## 概率基本公式
### 全概率公式
设 $B_1...B_n$ 是样本空间 $\Omega$ 的一个分割，那么对于任一事件 $A$ 有
$$
    P(A) = \sum_{k=1}^{n}P(AB_k)
$$

### 乘法公式
对任意事件$A,B$
$$
    P(AB) = P(B)P(A|B)
$$

### 贝叶斯公式
设 $B_1...B_n$ 是样本空间 $\Omega$ 的一个分割，那么
$$
P(B_i|A) = \frac{P(AB_i)}{\sum_{k=1}^{n} P(A|B_k)P(B_k)}
$$

# 随机变量
随机变量是指可以用来表示随机试验结果的变量。

***定义*** 称在概率空间 $(\Omega, \mathcal{F}, P)$ 上的函数 $X$ 为随机变量，若 $X: \Omega \to R$，同时对于每一个实数 $r$ 都有一个事件集合 $A_r$ 相对应且 $A_r = {\{e : X(e) \leq r \}}$。

## 离散型分布
## 连续型分布
### 正态分布(Normal distribution)
$$
    f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2}(\frac{x - \mu}{\sigma})^2}
$$
期望为 $\mu$，方差为 $\sigma^2$。若 $\mu=0, \sigma=1$ 则为标准正态分布。

# 随机过程
## 二次变分(Quadratic Variation)
设 $X_t$ 是实值随机过程，$t$ 是时间。二次变差 $[X]_t$ 定义为
$$
    [X]_t = \lim_{||P||->0} \sum_{k=1}^n (X_{t_k} - X_{t_{k-1}})^2
$$
其中 $||P||$ 是对区间 $[0, t]$ 的网格划分单元的二范数，即
$$
    t_n - t_0 = t \\
    (t_k - t_{k-1})^2 = ||P||
$$

### 连续可微函数的二次变分
根据微积分中值定理，对于一个在 $[0, T]$ 内处处连续可微的函数 $f(t)$，二次变分有
$$
    \sum_k (f(t_k) - f(t_{k-1}))^2 = \sum_k (t_k - t_{k-1})^2 f'(t_k)^2 \\
    \leq \max_{s \in [0,T]} f'(s)^2 \sum_k (t_k - t_{k-1})^2 \\
    \leq \max_{s \in [0,T]} f'(s)^2 \cdot \max_k \{t_k - t_{k-1}\} \cdot T = 0
$$
显然其二次变分为零。

# References
李育强 姚强. 应用随机过程.

[https://en.wikipedia.org/wiki/Quadratic_variation](https://en.wikipedia.org/wiki/Quadratic_variation)