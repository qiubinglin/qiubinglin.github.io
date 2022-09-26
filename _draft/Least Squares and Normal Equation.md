---
layout:     post
title:      "最小二乘与法线方程"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog: true
tags:
    - 最小二乘
    - 线性方程组
    - 法线
---
# 不一致系统
对于 $Ax = b$，其中 $A$ 为 $m \times n$ 阶矩阵，$x \in R^n, b \in R^m$。令 $A = [A_1,...,A_n]$，则有
$$
    Ax = b <=> x_1A_1 + ... + x_nA_n = b
$$
显然若 $m > n$，存在 $b \in R^m$ 使得方程 $Ax = b$ 无解。

# 最小二乘的法线方程
对于不一致系统
$$
    Ax = b
$$
求解
$$
    A^T A\overline{x} = A^T b
$$
$\overline{x}$ 便是系统的最小二乘解，它最小化余项 $b - Ax$ 的欧式长度。

