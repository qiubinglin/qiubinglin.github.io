---
layout:     post
title:      "Krylov子空间方法"
date:       2022-02-13 13:32:00
author:     "Bing"
catalog:    true
tags:
    - 数值计算
    - 矩阵计算
    - 最小二乘
    - 迭代方法
---
# Krylov子空间
先讲述大规模稀疏线性方程组

再引出Krylov子空间的概念

在讲讲Krylov子空间的一些性质

最后启下Arnoldi过程

# Arnoldi过程
## Arnoldi过程
这个过程无非就是求出 $\Kappa_m$ 的一组正交基，这里给出最常见的基于Gram-Schmidt正交化的实现。

这个过程其实也就是QR分解的过程，很多性质可以从QR分解的性质中直接得到。

## Arnoldi过程的性质

