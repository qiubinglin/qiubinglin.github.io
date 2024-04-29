---
layout:     post
title:      "Moore–Penrose Inverse"
date:       2024-04-29 10:04:00
author:     "Bing"
catalog:    true
tags:
    - 线性代数
---

# Pseudoinverse
For $A \in R^{m \times n}$, the pseudoinverse(Moore–Penrose inverse) of $A$ is defined as a matrix $A^+ \in R^{n \times m}$ satisfying all of the following criteria, known as Moore-Penrose conditions:
1. $AA^+$ maps all columns of $A$ to themselves.
$$
    AA^+ A = A
$$
2. $A^+$ acts like weak inverse.
$$
    A^+A A^+ = A^+
$$
3. $AA^+$ is Hermitian.
$$
    (AA^+)^* = AA^+
$$
4. $A^+A$ is Hermitian. 
$$
    (A^+A)^* = A^+A
$$

# Properties
## Existence and uniqueness
For any $A \in R^{m \times n}$, there is one and only one pseudoinverse $A^+ \in R^{n \times m}$.

## Useful properties
1. Pseudoinversion commutes with transposition, complex conjugation, and conjugate transposition.
$$
    (A^T)^+ = (A^+)^T \quad (\overline{A})^+ = \overline{(A^+)} \quad (A^*)^+ = (A^+)^*
$$
2. When $A$ has linearly independent columns
$$
    A^+ = (A^*A)^{-1}A^*
$$
When $A$ has linearly independent rows
$$
    A^+ = A^*(AA^*)^{-1}
$$

# References
[https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse)