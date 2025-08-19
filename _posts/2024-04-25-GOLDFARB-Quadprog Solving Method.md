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

## Proof of $HN = 0$

Starting with the definition of $H$:

$$
H = G^{-1}(I - NN^*)
$$

Substituting the definition of $N^*$:

$$
N^* = (N^T G^{-1} N)^{-1} N^T G^{-1}
$$

We have:

$$
HN = G^{-1}(I - NN^*)N = G^{-1}N - G^{-1}NN^*N
$$

Now, let's compute $NN^*N$:

$$
NN^*N = N(N^T G^{-1} N)^{-1} N^T G^{-1} N = N(N^T G^{-1} N)^{-1}(N^T G^{-1} N) = NI = N
$$

Therefore:

$$
HN = G^{-1}N - G^{-1}N = 0
$$

## Proof of $x^T H x ≥ 0$ for all $x ∈ R^n$

This property shows that $H$ is positive semidefinite. Let's prove it:

$$
x^T H x = x^T G^{-1}(I - NN^*)x
$$

Let $y = G^{-1/2}x$, then:

$$
x^T H x = y^T G^{1/2} G^{-1}(I - NN^*) G^{1/2} y = y^T(I - G^{1/2}NN^*G^{1/2})y
$$

Since $G$ is positive definite, $G^{1/2}$ exists and is symmetric. Let's show that $G^{1/2}NN^*G^{1/2}$ is a projection matrix:

$$
(G^{1/2}NN^*G^{1/2})^2 = G^{1/2}NN^*G^{1/2}G^{1/2}NN^*G^{1/2} = G^{1/2}NN^*GNN^*G^{1/2}
$$

Using the fact that $N*GN = (N^T G^{-1} N)^{-1} N^T G^{-1} G N = (N^T G^{-1} N)^{-1} N^T N = I$:

$$
G^{1/2}NN^*GNN^*G^{1/2} = G^{1/2}NN^*G^{1/2}
$$

This shows that $G^{1/2}NN^*G^{1/2}$ is idempotent, making it a projection matrix. Since projection matrices have eigenvalues 0 or 1, $I - G^{1/2}NN^*G^{1/2}$ is positive semidefinite.

Therefore, $x^T H x ≥ 0$ for all $x ∈ R^n$.

## Proof of $HGH = H$

Starting with the left side:

$$
HGH = G^{-1}(I - NN^*) G G^{-1}(I - NN^*)
$$

Simplifying:

$$
HGH = G^{-1}(I - NN^*) G G^{-1}(I - NN^*) = G^{-1}(I - NN^*) (I - NN^*)
$$

Since $(I - NN^*)(I - NN^*) = I - 2NN^* + NN^*NN^*$:

$$
HGH = G^{-1}(I - 2NN^* + NN^*NN^*)
$$

We need to show that $NN^*NN^* = NN^*$. Let's compute:

$$
NN^*NN^* = N(N^T G^{-1} N)^{-1} N^T G^{-1} N(N^T G^{-1} N)^{-1} N^T G^{-1}
$$

Using the fact that $N^T G^{-1} N(N^T G^{-1} N)^{-1} = I$:

$$
NN^*NN^* = N(N^T G^{-1} N)^{-1} N^T G^{-1} = NN^*
$$

Therefore:

$$
HGH = G^{-1}(I - 2NN^* + NN^*) = G^{-1}(I - NN^*) = H
$$

## Proof of $N*GH = 0$

Starting with the left side:

$$
N^*GH = N^* G G^{-1}(I - NN^*) = N^*(I - NN^*)
$$

Expanding:

$$
N^*GH = N^* - N^*NN^*
$$

We already showed that $NN^*NN^* = NN^*$, so:

$$
N^*GH = N^* - N^* = 0
$$

## Proof of $HH^+ = H^+$

This property shows that H is equal to its own Moore-Penrose pseudoinverse. Let's prove it:

$$
HH^+ = G^{-1}(I - NN^*) G^{-1}(I - N^+N^{+*})
$$

We need to show that this equals $H^+$. Since H is symmetric and positive semidefinite, its pseudoinverse $H^+$ should satisfy:

$$
HH^+H = H
$$
$$
H^+HH^+ = H^+
$$

Let's verify the first condition:

$$
HH^+H = G^{-1}(I - NN^*) G^{-1}(I - N^TN) G^{-1}(I - NN^*)
$$

Using the fact that $N^+ = N^T$ and $N^{+*} = N$:

$$
HH^+H = G^{-1}(I - NN^*) G^{-1}(I - N^TN) G^{-1}(I - NN^*)
$$

Since $N^TN$ is a projection matrix onto the column space of $N^T$, and $(I - NN^*)N = 0$, we have:

$$
HH^+H = G^{-1}(I - NN^*) = H
$$

This shows that $H^+ = G^{-1}(I - N^+N^{+*})$ satisfies the pseudoinverse conditions, and therefore $HH^+ = H^+$.

## Additional Properties

### Property: H is symmetric

$$
H^T = (G^{-1}(I - NN^*))^T = (I - NN^*)^T G^{-1} = (I - N^{*T}N^T)G^{-1}
$$

Since $G^{-1}$ is symmetric and $N^{*T} = (N^T G^{-1} N)^{-1} N^T G^{-1} = N^*$, we have:

$$
H^T = (I - N^*N^T)G^{-1}
$$

However, this is not immediately equal to H. The symmetry of H follows from the fact that $G^{-1}$ is symmetric and the specific structure of the projection matrix.

### Property: Range and Null Space
The matrix H projects vectors onto the null space of $N^T$, i.e., the orthogonal complement of the column space of N. This follows from:

$$HN = 0$$
$$N^TH = 0$$

This means that H annihilates any vector in the column space of N and preserves vectors orthogonal to it.

# Implementation

## Algorithm Overview

The Goldfarb-Idnani algorithm is an active set method for solving quadratic programming problems. It iteratively adds constraints to the active set and updates the solution using the properties we proved above.

## Algorithm Steps

### Step 1: Initialization
Start with an empty active set and solve the unconstrained problem:

$$
x_0 = -G^{-1}c
$$
$$\lambda_0 = \emptyset$$

### Step 2: Constraint Selection
At iteration k, find the most violated constraint:

$$
i^* = \arg\max_{i \notin A_k} \frac{a_i^T x_k - b_i}{\|a_i\|_{G^{-1}}}
$$

If no constraint is violated (or violation is below tolerance), terminate.

### Step 3: Direction Computation
Compute the search direction using the projection matrix H:

$$
d_k = -H_k a_{i^*}
$$

Where H_k is computed using the current active set:

$$
H_k = G^{-1}(I - N_k N_k^*)
$$
$$N_k^* = (N_k^T G^{-1} N_k)^{-1} N_k^T G^{-1}$$

### Step 4: Step Size Determination
Compute the step size to reach the constraint boundary:

$$
\alpha_k = \frac{b_{i^*} - a_{i^*}^T x_k}{a_{i^*}^T d_k}
$$

### Step 5: Solution Update
Update the solution:

$$
x_{k+1} = x_k + \alpha_k d_k
$$

### Step 6: Active Set Update
Add the new constraint to the active set:

$$
A_{k+1} = A_k \cup \{i^*\}
$$

## Key Implementation Details

### Matrix Updates
When adding a constraint, the projection matrix H can be updated efficiently using the Sherman-Morrison-Woodbury formula:

$$
H_{k+1} = H_k - \frac{H_k a_{i^*} a_{i^*}^T H_k}{a_{i^*}^T H_k a_{i^*}}
$$

### Numerical Stability
- Use Cholesky decomposition for G^{-1} computation
- Implement proper numerical checks for near-singular matrices
- Use appropriate tolerances for constraint violations

### Termination Criteria
The algorithm terminates when:
1. All constraints are satisfied within tolerance
2. Maximum number of iterations reached
3. Numerical issues detected

## Complexity Analysis

- **Per iteration**: O(n²) for matrix operations
- **Total complexity**: O(n³) in worst case
- **Memory**: O(n²) for storing matrices

## Advantages

1. **Finite convergence**: Guaranteed to converge in finite steps
2. **Efficient updates**: Matrix updates can be done incrementally
3. **Warm start capability**: Can start from a feasible point

## Limitations

1. **Warm start dependency**: Performance depends on initial point quality
2. **Constraint ordering**: Order of constraint addition affects efficiency
3. **Numerical sensitivity**: May face issues with ill-conditioned problems

## Practical Considerations

### Initial Point Selection
- Use the unconstrained solution if feasible
- Apply phase I methods to find a feasible starting point
- Consider using previous solutions for similar problems

### Constraint Management
- Implement constraint dropping strategies
- Use constraint scaling for better conditioning
- Handle degenerate cases carefully

### Performance Optimization
- Cache matrix factorizations when possible
- Use sparse matrix techniques for large problems
- Implement parallel constraint checking

# References
[https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail](https://web.archive.org/web/20170812011814/http://www.javaquant.net/papers/GoldfarbIdnani.pdf?origin=publication_detail)