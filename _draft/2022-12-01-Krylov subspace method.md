---
layout:     post
title:      "Krylov子空间方法"
date:       2022-12-01 13:32:00
author:     "Bing"
catalog:    true
tags:
    - 数值计算
    - 矩阵计算
    - 最小二乘
    - 迭代方法
---

在解 $n$ 维大型稀疏线性方程组 $Ax = b$ 时，使用直接求解的方法可能会很慢并且对内存占用很大，这时候就考虑其他的一些近似求解方法。

Krylov子空间方法是一种投影方法，即在 $m(m \ll n)$ 维空间中寻找真解的近似解，它非常适合于求解大型稀疏线性方程组。

# Krylov子空间
## 定义
设 $A \in R^{n \times n}$，$r \in R^n$，我们称
$$
    K_m(A, r) \triangleq span\{r, Ar, A^2r...A^{m-1}r\} \subseteq R^n
$$
是由 $A$ 和 $r$ 生成的Krylov子空间，简记为 $K_m$。

## 基本性质
Krylov子空间是嵌套的，即：$K_1 \subseteq K_2 \subseteq ... ... \subseteq K_m$

$dim(K_m) \leq m$

$K_m(A, r) = \{x = p(A)r：p是次数不超过m-1的多项式\}$

# Arnoldi过程
Arnoldi过程是构建 $K_m$ 的关键过程，即求出 $K_m$ 的一组正交基。这里给出最常见的基于Gram-Schmidt正交化的实现。

## Gram-Schmidt正交化Arnoldi过程


这个过程其实也就是对 $(r | Av_1 | Av_2 | ... |Av_{k-1})$ 做QR分解的过程。

## Arnoldi过程的性质

