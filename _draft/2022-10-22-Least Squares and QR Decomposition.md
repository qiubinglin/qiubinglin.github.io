---
layout:     post
title:      "最小二乘与QR分解"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog:    true
tags:
    - 数值计算
    - 矩阵计算
    - 最小二乘
    - QR分解
    - Gram-Schmidt正交化
---
# 什么是QR分解
## 方阵
任意实方阵 $A$ 都可以被分解为
$$
    A = QR
$$
其中 $Q$ 是正交矩阵（列向量与行向量皆为正交的单位向量），$R$ 是上三角矩阵。
如果 $A$ 是可逆的并限制 $R$ 的对角元素为正数，那么此分解是唯一的。

## 矩阵
更一般的，对于 $m \times n$ 的复数矩阵 $A$，$m \geq n$，我们可以将其分解成 $m \times m$ 的幺正矩阵 $Q$ 与 $m \times n$ 的上三角矩阵 $R$ 的乘积。
$$
    A = QR = Q \begin{bmatrix}
        R_1 \\
        0
    \end{bmatrix} = \begin{bmatrix}
        Q_1 & Q_2
    \end{bmatrix} \begin{bmatrix}
        R_1 \\
        0
    \end{bmatrix} = Q_1R_1
$$

# Gram-Schmidt正交化
