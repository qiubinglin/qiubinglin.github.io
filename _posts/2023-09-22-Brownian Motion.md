---
layout:     post
title:      "布朗运动"
date:       2023-09-22 17:42:00
author:     "Bing"
catalog:    true
tags:
    - 随机过程
---

# 马尔可夫过程(Markov Process)
假设随机过程 $[X_1, X_2,...]$ 有马尔可夫性质，下一个随机变量的分布仅依赖于当前随机变量，即
$$
    Pr(X_{n+1} | X_1 = x_1, X_2 = x_2..., X_n = x_n) = Pr(X_{n+1} | X_n = x_n)
$$
那么该随机过程为马尔可夫过程。

# 莱维过程(Lévy Process)

# 维纳过程(Wiener Process)
布朗运动在数学上被称为维纳过程(Wiener Process)，它具有如下性质
1. $W_0 = 0$
2. $W_t$ 是连续的
3. 独立增量性，$W_t$ 的增量是独立的
4. 平稳性，且 $W_t - W_s \sim N(0, t - s)$ 对于 $0 \leq s < t$

$N(\mu, \sigma^2)$ 是期望为 $\mu$，方差为 $\sigma^2$ 的标准正态分布。

## 维纳过程的二次变分
考虑维纳过程在区间 $[0, T]$ 的二次变分，有
$$
    \sum_k (W_{t_{k}} - W_{t_{k-1}})^2 = T
$$
微分形式则为
$$
    (dW_t)^2 = dt
$$

## 随机游走(Random Walk)
在足够的时间尺度下，随机游走近似于布朗运动。

## 几何布朗运动(Geometric Brownian motion)
考虑给标准布朗运动加上仅与时间相关的漂移项 $\mu t$，以及一个尺度参数 $\sigma$，得到一个带漂移的布朗运动
$$
    X_t = \mu t + \sigma B_t \\
    dX_t = \mu dt + \sigma dB_t
$$
其中 $B_t$ 是布朗运动。

显然 $X(T)$ 满足正态分布
$$
    X(T) \sim  N(X(0) + \mu, \sigma^2 T)
$$

### 描述股票价格
上述模型在描述股价时存在缺陷，因为股价不可能是负的，所以通常用 $X_t$ 描述股票收益率 $dS_t / S_t$，其中 $S_t$ 是股价。

***定义*** 随机过程 $S_t$ 是几何布朗运动(GBM)，当它满足以下随机微分方程
$$
    dS_t = \mu S_t dt + \sigma S_t dW_t
$$
其中 $W_t$ 是维纳过程。$\mu$ 是漂移率常数，$\sigma$ 是波动率常数。

若 $\sigma = 0$，显然 $\mu$ 即是股票的收益率。

# References
李育强 姚强. 应用随机过程.

[https://en.wikipedia.org/wiki/Markov_chain](https://en.wikipedia.org/wiki/Markov_chain)

[https://en.wikipedia.org/wiki/Wiener_process](https://en.wikipedia.org/wiki/Wiener_process)

[https://en.wikipedia.org/wiki/Geometric_Brownian_motion](https://en.wikipedia.org/wiki/Geometric_Brownian_motion)

[https://zhuanlan.zhihu.com/p/38293827](https://zhuanlan.zhihu.com/p/38293827)