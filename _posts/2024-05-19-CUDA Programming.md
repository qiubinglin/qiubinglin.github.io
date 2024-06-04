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

# Example
```
#include <stdio.h>
#include <stdlib.h>
#include <cuda_runtime.h>

__global__ void add(int n, float *x, float *y, float *z)
{
  int i = blockIdx.x*blockDim.x + threadIdx.x;
  if (i < n) z[i] = x[i] + y[i];
}

int main(void)
{
  int N = 1<<20;
  float *x, *y, *z, *d_x, *d_y, *d_z;
  x = (float*)malloc(N*sizeof(float));
  y = (float*)malloc(N*sizeof(float));
  z = (float*)malloc(N*sizeof(float));

  cudaMalloc(&d_x, N*sizeof(float));
  cudaMalloc(&d_y, N*sizeof(float));
  cudaMalloc(&d_z, N*sizeof(float));

  for (int i = 0; i < N; i++) {
        x[i] = rand()*1.0/RAND_MAX;
        y[i] = rand()*1.0/RAND_MAX;
  }

  cudaMemcpy(d_x, x, N*sizeof(float), cudaMemcpyHostToDevice);
  cudaMemcpy(d_y, y, N*sizeof(float), cudaMemcpyHostToDevice);

  add<<<(N+255)/256, 256>>>(N, d_x, d_y, d_z);

  cudaMemcpy(z, d_z, N*sizeof(float), cudaMemcpyDeviceToHost);

  float maxError = 0.0f;
  for (int i = 0; i < N; i++)
        maxError = max(maxError, fabs(z[i]-x[i]-y[i]));
  printf("Max error: %f\n", maxError);

  cudaFree(d_x);
  cudaFree(d_y);
  cudaFree(d_z);
  free(x);
  free(y);
  free(z);

  return 0;
}
```

# References
[https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model)