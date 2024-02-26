---
layout:     post
title:      "QR分解"
date:       2022-11-30 16:37:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 线性代数
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
设 $A$ 为 $m \times n$ 的实矩阵，$m \geq n$，
$$
    A = \{ A_1, A_2...A_n \}
$$
若 $A_1, A_2...A_n$ 线性无关，相应的Gram-Schmidt正交过程如下。

$$
    y_1 = A_1, q_1 = \frac{y_1}{||y_1||_2}
$$
$$
    y_2 = A_2 - q_1({q_1}^T A_2), q_2 = \frac{y_2}{||y_2||_2}
$$
$$
    y_j = A_j - q_1({q_1}^T A_j) - ... - q_{j-1}({q_{j-1}}^T A_j), q_j = \frac{y_j}{||y_j||_2}
$$
显然 $q_1 ... q_n$ 是一组单位正交向量。

令 
$$
r_{ii} = ||y_i||_2, r_{ij} = {q_i}^T A_j
$$
那么上述式子可以整理为
$$
    A_1 = r_{11}q_1
$$
$$
    A_2 = r_{12}q_1 + r_{22}q_2
$$
$$
    A_j = r_{1j}q_1 + r_{2j}q_2 + ... + r_{j-1,j}q_{j-1} + r_{jj}q_j
$$
写成矩阵形式
$$
    (A_1 | ... | A_n) = (q_1 | ... | q_n) \begin{bmatrix}
        r_{11} & r_{12} & ... & r_{1n} \\
        & r_{22} & ... & r_{2n} \\
        & & ... & ... \\
        & & & r_{nn}
    \end{bmatrix}
$$

于是我们完成了对 $A$ 的Gram-Schmidt正交化，并且得到了 $A$ 的QR分解。显然这个过程也是对QR分解命题的证明。