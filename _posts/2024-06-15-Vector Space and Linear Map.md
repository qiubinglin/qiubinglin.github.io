---
layout:     post
title:      "Vector Space and Linear Map"
date:       2024-06-15 10:09:00
author:     "Bing"
catalog:    true
tags:
    - 线性代数
    - 数学
    - 向量空间
---

# Vector Space

## Definition

A **vector space** over a field $\mathbb{F}$ (typically $\mathbb{R}$ or $\mathbb{C}$) is a set $V$ equipped with two operations:
- **Vector addition**: $+ : V \times V \to V$
- **Scalar multiplication**: $\cdot : \mathbb{F} \times V \to V$

These operations must satisfy the following axioms for all $u, v, w \in V$ and all scalars $a, b \in \mathbb{F}$:

### Axioms of Vector Addition
1. **Closure**: $u + v \in V$
2. **Commutativity**: $u + v = v + u$
3. **Associativity**: $(u + v) + w = u + (v + w)$
4. **Identity element**: There exists $0 \in V$ such that $v + 0 = v$ for all $v \in V$
5. **Inverse element**: For every $v \in V$, there exists $-v \in V$ such that $v + (-v) = 0$

### Axioms of Scalar Multiplication
6. **Closure**: $a \cdot v \in V$
7. **Distributivity over vector addition**: $a \cdot (u + v) = a \cdot u + a \cdot v$
8. **Distributivity over scalar addition**: $(a + b) \cdot v = a \cdot v + b \cdot v$
9. **Associativity**: $a \cdot (b \cdot v) = (ab) \cdot v$
10. **Identity**: $1 \cdot v = v$

## Examples of Vector Spaces

- $\mathbb{R}^n$: The set of all $n$-tuples of real numbers
- $\mathcal{P}_n(\mathbb{R})$: The set of all polynomials of degree at most $n$ with real coefficients
- $\mathcal{C}[a,b]$: The set of all continuous functions on the interval $[a,b]$

---

# Linear Map

## Definition

A **linear map** (or linear transformation) from vector space $V$ to vector space $W$ over the same field $\mathbb{F}$ is a function $T: V \to W$ that preserves the vector space operations:

1. **Additivity**: $T(u + v) = T(u) + T(v)$ for all $u, v \in V$
2. **Homogeneity**: $T(\lambda v) = \lambda T(v)$ for all $\lambda \in \mathbb{F}$ and $v \in V$

## Properties of Linear Maps

- $T(0_V) = 0_W$ (maps zero vector to zero vector)
- $T(-v) = -T(v)$ for all $v \in V$
- $T(a_1v_1 + a_2v_2 + \cdots + a_nv_n) = a_1T(v_1) + a_2T(v_2) + \cdots + a_nT(v_n)$

---

# Fundamental Theorem of Linear Maps

## Theorem

Let $V$ be a finite-dimensional vector space and $T \in \mathcal{L}(V, W)$ be a linear map. Then:
$$
\dim V = \dim(\ker T) + \dim(\text{range } T)
$$

where:
- $\ker T = \{v \in V : T(v) = 0\}$ is the **kernel** (null space) of $T$
- $\text{range } T = \{T(v) : v \in V\}$ is the **range** (image) of $T$

## Proof

Let $\{u_1, \ldots, u_m\}$ be a basis for $\ker T$. Extend this to a basis $\{u_1, \ldots, u_m, v_1, \ldots, v_n\}$ for $V$.

**Claim**: $\{T(v_1), \ldots, T(v_n)\}$ is a basis for $\text{range } T$.

### Proof of the Claim

1. **Spanning**: For any $w \in \text{range } T$, there exists $v \in V$ such that $T(v) = w$. Since $v$ can be written as:
   $$v = \sum_{i=1}^m a_i u_i + \sum_{j=1}^n b_j v_j$$
   
   We have:
   $$w = T(v) = \sum_{i=1}^m a_i T(u_i) + \sum_{j=1}^n b_j T(v_j) = \sum_{j=1}^n b_j T(v_j)$$
   
   (Note: $T(u_i) = 0$ since $u_i \in \ker T$)

2. **Linear Independence**: Suppose $\sum_{j=1}^n c_j T(v_j) = 0$. Then:
   $$T\left(\sum_{j=1}^n c_j v_j\right) = 0$$
   
   This implies $\sum_{j=1}^n c_j v_j \in \ker T$, so:
   $$\sum_{j=1}^n c_j v_j = \sum_{i=1}^m d_i u_i$$
   
   Since $\{u_1, \ldots, u_m, v_1, \ldots, v_n\}$ is a basis, we must have $c_j = 0$ for all $j$.

Therefore, $\dim(\text{range } T) = n$, and the theorem follows.

---

# Linear Maps and Matrices

## Matrix Representation

### Definition: Matrix

An **$m \times n$ matrix** $A$ over a field $\mathbb{F}$ is a rectangular array of elements from $\mathbb{F}$:

$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$

### Definition: Matrix of a Linear Map

Let $T \in \mathcal{L}(V, W)$ be a linear map, and let:
- $\mathcal{B}_V = \{v_1, \ldots, v_n\}$ be a basis for $V$
- $\mathcal{B}_W = \{w_1, \ldots, w_m\}$ be a basis for $W$

The **matrix representation** of $T$ with respect to these bases, denoted $[T]_{\mathcal{B}_V}^{\mathcal{B}_W}$, is the $m \times n$ matrix whose $(i,j)$-entry is defined by:

$$
T(v_j) = \sum_{i=1}^m a_{ij} w_i
$$

That is, the $j$-th column of $[T]_{\mathcal{B}_V}^{\mathcal{B}_W}$ contains the coordinates of $T(v_j)$ with respect to the basis $\mathcal{B}_W$.

### Definition: Matrix of a Vector

Let $v \in V$ and $\mathcal{B}_V=\{v_1, \ldots, v_n\}$ be a basis for $V$. If $v = \sum_{i=1}^n a_i v_i$, then the **coordinate vector** of $v$ with respect to $\mathcal{B}_V$ is:

$$
[v]_{\mathcal{B}_V} = \begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_n
\end{pmatrix}
$$

## Matrix Operations and Linear Maps

### Composition of Linear Maps

If $T: V \to W$ and $S: W \to U$ are linear maps, then:

$$
[S \circ T]_{\mathcal{B}_V}^{\mathcal{B}_U} = [S]_{\mathcal{B}_W}^{\mathcal{B}_U} \cdot [T]_{\mathcal{B}_V}^{\mathcal{B}_W}
$$

### Change of Basis

If $\mathcal{B}_V'$ and $\mathcal{B}_W'$ are different bases for $V$ and $W$ respectively, then:

$$
[T]_{\mathcal{B}_V'}^{\mathcal{B}_W'} = P_W^{-1} \cdot [T]_{\mathcal{B}_V}^{\mathcal{B}_W} \cdot P_V
$$

where $P_V$ and $P_W$ are the change-of-basis matrices.

---

# Applications and Examples

## Example 1: Rotation in $\mathbb{R}^2$

Consider the rotation map $T: \mathbb{R}^2 \to \mathbb{R}^2$ that rotates vectors by angle $\theta$:

$$T\begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} x\cos\theta - y\sin\theta \\ x\sin\theta + y\cos\theta \end{pmatrix}$$

With respect to the standard basis $\{e_1, e_2\}$, the matrix representation is:

$$[T] = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$$

## Example 2: Differentiation Operator

Let $T: \mathcal{P}_2(\mathbb{R}) \to \mathcal{P}_1(\mathbb{R})$ be the differentiation operator $T(p) = p'$.

With respect to the bases $\{1, x, x^2\}$ for $\mathcal{P}_2(\mathbb{R})$ and $\{1, x\}$ for $\mathcal{P}_1(\mathbb{R})$:

$$
[T] = \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \end{pmatrix}
$$

---

# References

- Axler, Sheldon. *Linear Algebra Done Right*. 3rd Edition, Springer, 2015.
- Lay, David C., et al. *Linear Algebra and Its Applications*. 5th Edition, Pearson, 2016.
- Strang, Gilbert. *Introduction to Linear Algebra*. 5th Edition, Wellesley-Cambridge Press, 2016.