---
layout:     post
title:      "Householder变换"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog:    true
tags:
    - 数学
    - 数值分析
    - QR分解
    - 最小二乘
---
# 投影矩阵
向量 $v$ 的投影矩阵为
$$
    P = \frac{v v^T}{v^T v}
$$
对于任意向量 $u$，$Pu$ 是 $u$ 在 $v$ 上的投影。

# Householder变换
***引理***
假设向量 $x$ 和 $w$ 具有相同的欧几里得范数，$||x||^2 = ||w||^2$，那么向量 $w-x$ 和 $w+x$ 正交。

定义 $v = w - x$，考虑投影矩阵 $P = \frac{v v^T}{v^T v}$，根据下图可以想到 $x - 2Px = w$，令 $H = I - 2P$，验证如下
$$
    Hx = x - 2Px = 
$$

