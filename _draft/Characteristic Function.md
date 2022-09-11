---
layout:     post
title:      "特征函数"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog: true
tags:
    - 概率论
    - 随机变量
    - 概率分布
    - 特征函数
---
有三个用于刻画随机变量的常用工具：特征函数、拉普拉斯变换和概率母函数

# 特征函数
定义。
设随机变量 $X$ 的分布函数是 $F$。我们称复值函数
$$
    \psi(t) = E(e^{itX})= \int_{-\infin}^{\infin} {e^{itX}dF(X)} \\
    = E(cos(tX)) + iE(sin(tX))
$$
为随机变量 $X$（或分布 $F$）的特征函数，其中 $t \in (-\infin, \infin)$。

# 拉普拉斯变换
定义。
若 $X$ 为非负随机变量，称函数
$$
    L_x(\theta) = E(e^{-\theta X})
$$
为 $X$ 的拉普拉斯变换， $\theta \in [0, \infin)$。

# 概率母函数
定义。
若 $X$ 是非负整数值的随机变量，称函数
$$
    \phi_X(s) = E(s^X)
$$
为 $X$ 的概率母函数，其中 $s \in [-1, 1]$。