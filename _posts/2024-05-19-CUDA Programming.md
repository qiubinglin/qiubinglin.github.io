---
layout:     post
title:      "CUDA Programming"
date:       2024-05-19 16:00:00
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

# Thread hierachy
![](/img/post/grid-of-thread-blocks.png)

```
int main()
{
    ...
    // Kernel invocation with grid_size=M, block_size=N
    VecAdd<<<M, N>>>(A, B, C);
    ...
}
```

# Device function
The function specified by ``__device__`` can be called in GPU, the function specified by ``__host__`` can be called in CPU.

```
__device__ int device_add(int a, int b) {
    return a + b;
}

__host__ int host_add(int a, int b) {
    return a + b;
}

__device__ int device_add(int a, int b) {
    return a + b;
}

__host__ __device__ int add(int a, int b) {
    return a + b;
}
```

``device_add`` can only be called in GPU, ``host_add`` can only be called in CPU, ``add`` can be called both in CPU and GPU.

# Compiling


# References
[https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model)