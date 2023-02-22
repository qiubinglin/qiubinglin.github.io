---
layout:     post
title:      "Jacobi方法与Gauss–Seidel方法"
date:       2023-02-17 16:57:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 矩阵计算
    - 方程组
    - 迭代方法
---

# Jacobi方法
Jacobi方法是线性方程组系统中的不动点迭代。

对于 $Ax = b$，令 $A = D + L + U$，$D$ 是主对角线矩阵，$L$ 是下三角矩阵（主对角线以下元素），$U$ 是上三角矩阵（主对角线以上元素）。有
$$
    Ax = b \\
    (D + L + U)x = b \\
    Dx = b - (L + U)x \\
    x = D^{-1}(b - (L + U)x)
$$
Jacobi方法为
$$
    x_0 = 初始向量 \\
    x_{k+1} = D^{-1}(b - (L + U)x_k)
$$

***定义***
$n \times n$ 的矩阵 $A = (a_{ij})$ 是严格对角占优矩阵，当且仅当对于任意 $1 \leq i \leq n$ 有 $|a_{ii}| > \sum_{j \neq i}|a_{ij}|$。

***定理***
如果$n \times n$ 的矩阵 $A = (a_{ij})$ 是严格对角占优矩阵，那么

（1）$A$ 是非奇异矩阵。

（2）对于任意向量 $b$ 和初值估计 $x_0$，对 $Ax = b$ 应用Jacobi方法都可以收敛到唯一解。

# Gauss–Seidel方法
Jacobi方法的变形
$$
    x_0 = 初始向量 \\
    x_{k+1} = D^{-1}(b - Ux_k - Lx_{k+1})
$$
整理得
$$
    x_{k+1} = -(D + L)^{-1} Ux_k + (D + L)^{-1}b
$$

***定理***
如果$n \times n$ 的矩阵 $A = (a_{ij})$ 是严格对角占优矩阵，那么

（1）$A$ 是非奇异矩阵。

（2）对于任意向量 $b$ 和初值估计 $x_0$，对 $Ax = b$ 应用Gauss–Seidel方法都可以收敛到唯一解。

# 连续过松弛(SOR)
连续过松弛(SOR)方法使用Gauss–Seidel方法的求解方向，并使用过松弛加快收敛速度。
$$
    x_0 = 初始向量 \\
    x_{k+1} = (\omega L + D)^{-1} [(1-\omega)Dx_k - \omega Ux_k] + \omega (D + \omega L)^{-1} b
$$
$\omega = 1$ 时即为Gauss–Seidel方法。