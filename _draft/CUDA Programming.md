---
layout:     post
title:      "CUDA Programming"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - GPU
    - CUDA
---

# Kernels
Let's see an example of CUDA kernel below
```
// Kernel definition
__global__ void VecAdd(float* A, float* B, float* C)
{
    int i = threadIdx.x;
    C[i] = A[i] + B[i];
}

int main()
{
    ...
    // Kernel invocation with N threads
    VecAdd<<<1, N>>>(A, B, C);
    ...
}
```
A kernel is defined using ``__global__`` declaration specifier and the number of CUDA threads that execute the kernel for a given kernel call is specified using a ``<<<...>>>`` execution configuration syntax. Each thread that executes the kernel is given a unique thread ID.

# Device function

# Compiling

# References
[https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model)