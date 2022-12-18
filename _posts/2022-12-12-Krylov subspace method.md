---
layout:     post
title:      "Krylov子空间方法"
date:       2022-12-12 14:50:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 矩阵计算
    - 最小二乘
    - 迭代方法
---

在解 $n$ 维大型稀疏线性方程组 $Ax = b$ 时，使用直接求解的方法可能会很慢并且对内存占用很大，这时候就考虑其他的一些近似求解方法。

Krylov子空间方法是一种[投影方法](https://qiubinglin.github.io/2022/11/27/Projection-Method-in-Matrix-Computation/)，即在 $m(m \ll n)$ 维空间中寻找真解的近似解，它非常适合于求解大型稀疏线性方程组。

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
<pre class="pseudocode">
\begin{algorithm}
\caption{Arnoldi}
\begin{algorithmic}
\PROCEDURE{Arnoldi}{$A, r, m$}
    \STATE 确认 $r$ 为非零向量，计算 $v_1 = r/||r||_2$
    \FOR{$j = 1,2...m-1$}
        \STATE $w_j = Av_j$
        \FOR{$i = 1,2...j$}
            \STATE $h_{i,j} = (w_j, v_i)$
        \ENDFOR
        \STATE $w_j = w_j - \sum_{i=1}^{j} h_{i,j}w_j$
        \STATE $h_{j+1,j} = ||w_j||_2$
        \IF{$h_{j+1,j} = 0$}
            \STATE break
        \ENDIF
        \STATE $v_{j+1} = w_j / h_{j+1,j}$
    \ENDFOR
\ENDPROCEDURE
\end{algorithmic}
\end{algorithm}
</pre>

这个过程其实也就是对
$$
(r|Av_1|Av_2|...|Av_{k-1})
$$
做QR分解的过程。

## Arnoldi过程的性质
***定理*** 如果Arnoldi过程不提前终止，则向量 $v_1,...v_m$ 构成 $K_m$ 的一组标准正交基，其中
$$
    K_m(A, r) = span\{r, Ar, ..., Ar^{m-1}\}
$$

***定理*** 设 $V_m = [v_1, v_2,..., v_m]$，则
$$
    AV_m = V_{m+1}H_{m+1,m} = V_mH_m + h_{m+1,m}v_{m+1}e_m^T
$$
$$
    V_m^T A V_m = H_m
$$
其中 $e_m = [0,...,0,1] \in R^m$，$H_m = H_{m+1,m}(1:m)(1:m) \in R^{m \times m}$，即 $H_m$ 是 $H_{m+1,m}$ 的前 $m$ 行组成的 $Hessenberg$ 矩阵。

***定理*** 如果Arnoldi过程在第 $k(k \leq m)$ 终止，即 $h_{k+1,k} = 0$，那么
$$
    AV_k = V_k H_k
$$
即 $K_k$ 是 $A$ 的一个不变子空间。

以上这些性质既可以通过Arnoldi过程直接推导出，也可以利用QR分解的性质证明。