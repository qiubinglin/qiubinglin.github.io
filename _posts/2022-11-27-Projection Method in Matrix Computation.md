---
layout:     post
title:      "投影方法-矩阵计算"
date:       2022-11-27 11:50:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 线性代数
---

# 问题
若线性方程组
$$
    Ax = b, A \in R^{n \times n}, b \in R^n
$$
非常巨大，无法直接求解，那么需要折衷地求解方程组的近似解。

投影方法是一种近似地求解线性方程组的数学方法，它可以这样来表述
# 表述
设 $K$ 是 $R^n$ 的一个子空间，记 $m \triangleq dim(K) \ll n$，投影方法的目标是在 $K$ 中寻找真解的一个“最佳”近似，显然近似解存在 $m$ 个自由度，因此需要设置 $m$ 个约束条件，在这里是
$$
    (r = b - A \overline{x}) \bot L
$$
$m$ 个正交约束条件，$b - A \overline{x}$是残差，$L$ 是另一个 $m$ 维的子空间。

通常来说，投影方法的关键在于确定投影空间 $K$ 与约束空间 $L$。

# 计算近似解
设 $V = \{v_1, v_2...v_m\}$ 和 $W = \{w_1, w_2...w_m\}$ 分别是 $K$ 和 $L$ 的一组基。
$\overline{x} = x^{(0)} + x_K$，$x_K$ 是 $K$ 中的一个向量，则由 $x_K = Vy$，以及正交性条件 $r_0 - AVy \bot w_i$，则有
$$
    W^TAVy = W^Tr_0
$$
若 $W^TAV$ 非奇异，则
$$
    y = (W^TAV)^{-1}W^Tr_0
$$


# 近似解的存在性
近似解存在当且仅当矩阵 $W^TAV$ 非奇异。

***定理***
如果 $A, K, L$ 满足以下条件之一

(1) $A$ 正定且 $L = K$

(2) $A$ 非奇异且 $L = AK$

则矩阵 $W^TAV$ 非奇异。

# References
Timothy Sauer. Numerical Analysis. Chapter 4.