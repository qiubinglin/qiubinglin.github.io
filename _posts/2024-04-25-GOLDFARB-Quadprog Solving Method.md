---
layout:     post
title:      "GOLDFARB-Quadprog Solving Method"
date:       2024-04-25 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 线性代数
---

# Basic Idea
Using Lagrange-Multiplier method and Newton's method to determine direction and step when adding every constrain.

# Notation
$$
    N^* = (N^T G^{-1} N)^{-1} N^T G^{-1}
    \\
    H = G^{-1}(I - NN^*)
$$

# Properties
$$
    HN = 0
    \\
    x^T H x \geq 0 \quad x \in R^n
    \\
    HGH = G^{-1}(I - NN^*) G G^{-1}(I - NN^*) = H
    \\
    N^*GH = N^* G G^{-1}(I - NN^*) = 0
    \\
    HH^+ = G^{-1}(I - NN^*) G^{-1}(I - N^+N^{+*}) = H^+
$$

# Proofs

# Implementation

# References
[https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail](https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail)