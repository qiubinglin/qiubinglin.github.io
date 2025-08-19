---
layout:     post
title:      "CUDA Programming Fundamentals"
date:       2024-03-19 16:00:00
author:     "Bing"
catalog:    true
tags:
    - GPU
    - CUDA
    - Parallel Computing
---

# Introduction to CUDA Programming

CUDA (Compute Unified Device Architecture) is NVIDIA's parallel computing platform that enables developers to use GPUs for general-purpose computing. This article covers the fundamental concepts of CUDA programming.

## What is CUDA?

CUDA allows you to write programs that can execute on NVIDIA GPUs, leveraging their massive parallel processing capabilities for computationally intensive tasks like scientific computing, machine learning, and graphics processing.

---

# CUDA Kernels

A CUDA kernel is a function that runs on the GPU device. It's the core concept in CUDA programming.

## Basic Kernel Definition

```cuda
// Kernel definition
__global__ void VecAdd(float* A, float* B, float* C)
{
    int i = threadIdx.x;
    C[i] = A[i] + B[i];
}
```

## Kernel Invocation

```cuda
int main()
{
    // Method 1: Simple invocation with N threads
    VecAdd<<<1, N>>>(A, B, C);

    // Method 2: Explicit grid and block dimensions
    dim3 grid_dim(1, 1, 1);
    dim3 block_dim(N, 1, 1);
    VecAdd<<<grid_dim, block_dim>>>(A, B, C);
}
```

### Key Points:
- **`__global__`**: Declares a kernel function that runs on the GPU
- **`<<<...>>>`**: Execution configuration syntax
- **Thread ID**: Each thread gets a unique identifier via `threadIdx.x`

---

# Thread Hierarchy

CUDA uses a hierarchical thread organization:

![CUDA Thread Hierarchy](/img/post/grid-of-thread-blocks.png)

## Thread Organization

```cuda
int main()
{
    // Kernel invocation with M blocks, N threads per block
    VecAdd<<<M, N>>>(A, B, C);
}
```

### Thread Hierarchy Levels:
1. **Thread**: Basic unit of execution
2. **Block**: Group of threads that can cooperate
3. **Grid**: Collection of blocks

### Thread Identification:
```cuda
__global__ void example_kernel()
{
    int tid = blockIdx.x * blockDim.x + threadIdx.x;
    // tid gives unique thread ID across the entire grid
}
```

---

# Function Qualifiers

CUDA provides different function qualifiers to control where functions can be called and executed:

## Function Types

```cuda
// Device-only function (GPU only)
__device__ int device_add(int a, int b) {
    return a + b;
}

// Host-only function (CPU only)
__host__ int host_add(int a, int b) {
    return a + b;
}

// Universal function (both CPU and GPU)
__host__ __device__ int add(int a, int b) {
    return a + b;
}
```

### Qualifier Meanings:
- **`__device__`**: Can only be called from GPU kernels
- **`__host__`**: Can only be called from CPU code
- **`__host__ __device__`**: Can be called from both CPU and GPU
- **`__global__`**: Kernel function that runs on GPU

---

# Complete CUDA Example

Here's a complete working example demonstrating vector addition:

```cuda
#include <stdio.h>
#include <stdlib.h>
#include <cuda_runtime.h>

// CUDA kernel for vector addition
__global__ void vector_add(int n, float *x, float *y, float *z)
{
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    if (i < n) {
        z[i] = x[i] + y[i];
    }
}

int main(void)
{
    int N = 1 << 20;  // 1M elements
    float *x, *y, *z, *d_x, *d_y, *d_z;
    
    // Allocate host memory
    x = (float*)malloc(N * sizeof(float));
    y = (float*)malloc(N * sizeof(float));
    z = (float*)malloc(N * sizeof(float));
    
    // Allocate device memory
    cudaMalloc(&d_x, N * sizeof(float));
    cudaMalloc(&d_y, N * sizeof(float));
    cudaMalloc(&d_z, N * sizeof(float));
    
    // Initialize host arrays
    for (int i = 0; i < N; i++) {
        x[i] = (float)rand() / RAND_MAX;
        y[i] = (float)rand() / RAND_MAX;
    }
    
    // Copy data from host to device
    cudaMemcpy(d_x, x, N * sizeof(float), cudaMemcpyHostToDevice);
    cudaMemcpy(d_y, y, N * sizeof(float), cudaMemcpyHostToDevice);
    
    // Launch kernel
    int block_size = 256;
    int grid_size = (N + block_size - 1) / block_size;
    vector_add<<<grid_size, block_size>>>(N, d_x, d_y, d_z);
    
    // Copy result back to host
    cudaMemcpy(z, d_z, N * sizeof(float), cudaMemcpyDeviceToHost);
    
    // Verify results
    float max_error = 0.0f;
    for (int i = 0; i < N; i++) {
        max_error = fmaxf(max_error, fabsf(z[i] - x[i] - y[i]));
    }
    printf("Max error: %f\n", max_error);
    
    // Cleanup
    cudaFree(d_x);
    cudaFree(d_y);
    cudaFree(d_z);
    free(x);
    free(y);
    free(z);
    
    return 0;
}
```

### Key Concepts Demonstrated:
1. **Memory Management**: `cudaMalloc`, `cudaMemcpy`, `cudaFree`
2. **Kernel Launch**: Grid and block size calculation
3. **Thread Coordination**: Each thread processes one element
4. **Error Checking**: Verification of results

---

# Memory Management

## Memory Types

- **Global Memory**: Large, high-latency memory accessible by all threads
- **Shared Memory**: Fast, per-block memory for thread cooperation
- **Local Memory**: Per-thread private memory
- **Constant Memory**: Read-only memory cached for all threads

## Best Practices

1. **Coalesced Memory Access**: Threads should access consecutive memory locations
2. **Shared Memory Usage**: Use shared memory for frequently accessed data
3. **Memory Bandwidth**: Minimize memory transactions

---

# Performance Considerations

## Optimization Techniques

1. **Occupancy**: Maximize the number of active warps per SM
2. **Memory Coalescing**: Ensure aligned, sequential memory access
3. **Shared Memory**: Use shared memory to reduce global memory access
4. **Warp Divergence**: Minimize conditional branching within warps

## Profiling Tools

- **NVIDIA Visual Profiler**: Performance analysis
- **nvprof**: Command-line profiler
- **NVIDIA Nsight**: Integrated development environment

---

# Common Pitfalls

1. **Forgetting Error Checking**: Always check CUDA API return values
2. **Memory Leaks**: Ensure `cudaFree` is called for all allocated memory
3. **Synchronization Issues**: Understand when kernels complete execution
4. **Grid/Block Size**: Choose appropriate dimensions for your hardware

---

# References

- [NVIDIA CUDA Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model)
- [CUDA C++ Best Practices Guide](https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/)
- [CUDA Runtime API Reference](https://docs.nvidia.com/cuda/cuda-runtime-api/)