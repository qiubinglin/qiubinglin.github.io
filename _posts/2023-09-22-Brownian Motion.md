---
layout:     post
title:      "布朗运动"
date:       2023-09-22 17:42:00
author:     "Bing"
catalog:    true
tags:
    - 随机分析
    - 随机过程
---

# 马尔可夫过程(Markov Process)

# Lévy Process

# 维纳过程(Wiener Process)
布朗运动在数学上被称为维纳过程(Wiener Process)，它具有如下性质
1. $W_0 = 0$
2. $W_t$ 是连续的
3. 独立增量性，$W_t$ 的增量是独立的
4. 平稳性，$W_t - W_s \sim N(0, t - s)$ 对于 $0 \leq s < t$

$N(\mu, \sigma^2)$ 是期望为 $\mu$，方差为 $\sigma^2$ 的标准正态分布。

## 维纳过程的二次变分

## 随机游走(Random Walk)
在足够的时间尺度下，随机游走近似于布朗运动。

## 几何布朗运动(Geometric Brownian motion)
随机过程 $S_t$ 是几何布朗运动(GBM)，当它满足以下随机微分方程
$$
    dS_t = \mu S_t dt + \sigma S_t dW_t
$$
其中 $W_t$ 是维纳过程。$\mu$ 是漂移率常数，$\sigma$ 是波动率常数。