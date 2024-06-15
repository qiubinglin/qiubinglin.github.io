---
layout:     post
title:      "Vector Space and Linear Map"
date:       2024-06-15 10:09:00
author:     "Bing"
catalog:    true
tags:
    - 线性代数
---

# Vector Space
***Definition***
A vector space is a set $V$ with the following properties hold:

1. $u + v \in V$, if $u,v \in V$.
2. $\lambda v \in V$, if $\lambda \in R, v \in V$.
3. $u + v = v + u$, for all $u,v \in V$.
4. $(u + v) + w = u + (v + w)$ and $(ab)v = a(bv)$, for all $u, v, w \in V$ and $a, b \in R$.
5. there exists an element $0 \in V$ such that $v + 0 = v$ for all $v \in V$.
6. for every $v \in V$, there exists an element $w \in V$ such that $v + w = 0$.
7. $1v = v$, for all $v \in V$.
8. $a(u + v) = au + av$ and $(a + b)v = av + bv$ for all $a,b \in R$ and $u,v \in V$.

# Linear Map
A linear map from $V$ to $W$ is a function $T: V \to W$ with the following properties:

1. $T(u + v) = Tu + Tv$ for all $u, v \in V$.
2. $T(\lambda v) = vT(v)$ for all $\lambda \in R$ and $v \in V$.

# Fundamental Theorem of Linear Maps
## Theorem

Suppose $V$ is finite-dimensional and $T \in \mathcal{L}(V, W)$. Then the range of T is finite-dimensional and
$$
    dim \; V = dim \; null \; T + dim \; range \; T
$$

## Proof
Let $u_1,...u_m$ be a basis of $null \; T$, then a basis of $V$ can be expressed as
$$
    u_1,...,u_m,v_1,...,v_n
$$
So for any vector in $V$
$$
    T(a_1u_1+...+a_mu_m + b_1v_1+...+b_nv_n) = b_1 Tv_1 + ... + b_n Tv_n
$$
Obviously, $Tv_1,...,Tv_n$ span range $T$ and is linearly independent because
$$
    c_1Tv_1 + ... + c_nT_n = 0
    \\
    T(c_1v_1 + ... + c_nv_n) = 0
    \\
    c_i = 0
$$
Hence, the theorem is proved.

# References
Linear Algebra Done Right. Chapter 1, 2 and 3.