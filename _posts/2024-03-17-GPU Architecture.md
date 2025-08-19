---
layout:     post
title:      "GPU Architecture: Understanding Modern Graphics Processing Units"
date:       2024-03-17 16:25:00
author:     "Bing"
catalog:    true
tags:
    - GPU
    - CUDA
    - Computer Architecture
    - Parallel Computing
---

# Introduction to GPU Architecture

Graphics Processing Units (GPUs) have evolved from simple graphics rendering devices to powerful parallel computing engines. This article explores the fundamental architecture of modern GPUs and how they differ from traditional CPUs.

## The GPU Philosophy

![CPU vs GPU Architecture](/img/post/gpu-devotes-more-transistors-to-data-processing.png "CPU vs GPU: Different Design Philosophies")

**"Thousands of cheap workers are better than one expensive all-rounder."**

This principle drives GPU design: instead of a few powerful, complex cores, GPUs use many simple, efficient cores optimized for parallel workloads.

---

# SIMT Architecture

**SIMT (Single Instruction, Multiple Threads)** is the execution model that combines the benefits of SIMD (Single Instruction, Multiple Data) with multithreading.

## How SIMT Works

- **Single Instruction**: All threads in a warp execute the same instruction simultaneously
- **Multiple Threads**: Each thread maintains its own execution state and can branch independently
- **Hardware Efficiency**: Maximizes instruction throughput while maintaining flexibility

---

# GPU Hardware Architecture

## Overall GPU Structure

![Complete GPU Architecture](/img/post/GPU-Hardware.jpg)

Modern GPUs consist of multiple Streaming Multiprocessors (SMs) connected through a sophisticated memory hierarchy.

## Simplified GPU Layout

![Simple GPU Architecture](/img/post/simple_gpu_arch.png)

### Data Flow
1. **Host CPU** sends tasks to GPU
2. **Tasks** are distributed across multiple SMs
3. **Data** flows through: DRAM → L2 Cache → L1 Cache → SMs
4. **Instructions** are executed in parallel across SMs

---

# Streaming Multiprocessors (SMs)

![SM Internal Structure](/img/post/GPU-SM.jpg)

## SM Components

### **Processing Units**
1. **Arithmetic Logic Units (ALUs)**: Handle integer operations
2. **Floating Point Units (FPUs)**: Execute floating-point calculations
3. **Special Function Units (SFUs)**: Handle transcendental functions (sin, cos, log, etc.)
4. **Load/Store Units (LD/ST)**: Manage memory operations

### **Memory & Control**
5. **Register File**: Fast local storage for thread data
6. **Warp Scheduler & Dispatch Unit**: Manage thread execution
7. **Tensor Cores**: Specialized units for AI/ML operations
8. **L1 Cache**: Fast local memory for the SM
9. **Texture Units (Tex)**: Optimized for texture sampling operations
10. **Ray Tracing Cores (RT)**: Accelerate ray-traced graphics rendering

---

# Thread Execution Model

## Thread Block Placement

![SM Utilization](/img/post/utilize-8sm-gpu.png)

At runtime, thread blocks are distributed across available SMs:
- Each SM can host multiple thread blocks
- Threads within a block can communicate and synchronize efficiently
- SMs automatically balance workload distribution

## Warp Execution

![Warp Divergence Example](/img/post/warp-divergence-example.png)

### Warp Characteristics
- **Size**: 32 threads per warp (standard across modern NVIDIA GPUs)
- **Execution**: All threads in a warp execute the same instruction simultaneously
- **Branching**: Individual threads can branch independently, but this causes warp divergence
- **Efficiency**: Warps with similar execution paths achieve maximum performance

### Warp Divergence
When threads in a warp take different execution paths:
- **Performance Impact**: Reduced efficiency as some threads are idle
- **Best Practice**: Minimize conditional branching within warps
- **Alternative**: Use warp-level primitives for conditional execution

---

# Memory Hierarchy & Access Patterns

## Global Memory

### Access Requirements
- **Supported Sizes**: 1, 2, 4, 8, or 16 bytes
- **Alignment**: Data must be naturally aligned (address multiple of data size)
- **Default Alignment**: Allocated memory is aligned to at least 256 bytes

### Performance Characteristics
- **High Latency**: Slowest memory in the hierarchy
- **High Bandwidth**: Can transfer large amounts of data
- **Coalescing**: Multiple threads accessing consecutive addresses achieve maximum bandwidth

## Shared Memory

### Bank Organization
- **32 Banks**: Organized for 32-bit word access
- **Bank Bandwidth**: 32 bits per clock cycle per bank
- **Conflict-Free Access**: Threads accessing different banks achieve maximum throughput

### Access Patterns
```
Bank 0: Thread 0, Thread 32, Thread 64, ...
Bank 1: Thread 1, Thread 33, Thread 65, ...
...
Bank 31: Thread 31, Thread 63, Thread 95, ...
```

## Warp Memory Access

![Warp Memory Access Pattern 1](/img/post/gpu-warp-memory-access1.png)

![Warp Memory Access Pattern 2](/img/post/gpu-warp-memory-access2.png)

### Optimal Access Pattern
- **Bandwidth**: 128 bytes per clock cycle (32 threads × 4 bytes)
- **Alignment**: Memory addresses should be aligned to 128-byte boundaries
- **Coalescing**: Sequential, aligned access maximizes memory throughput

---

# Performance Characteristics

## Latency vs Throughput

| Aspect | CPU | GPU |
|--------|-----|-----|
| **Latency** | Low | High |
| **Throughput** | Moderate | Very High |
| **Use Case** | Serial tasks | Parallel workloads |

### Why This Trade-off?
- **CPU**: Optimized for low-latency, single-thread performance
- **GPU**: Optimized for high-throughput, parallel execution
- **Result**: GPUs excel at data-parallel applications despite higher latency

## Thread Switching

### Register-Based Context Switching
- **Efficiency**: GPU switches threads by swapping register contents only
- **Speed**: Much faster than traditional context switching
- **Scalability**: Enables thousands of concurrent threads

---

# Specialized Processing Units

## CUDA Cores vs Tensor Cores

### CUDA Cores
- **Purpose**: General-purpose parallel computing
- **Operations**: Integer and floating-point arithmetic
- **Flexibility**: Handle diverse computational workloads
- **Programming**: Standard CUDA programming model

### Tensor Cores
- **Purpose**: Deep learning and AI acceleration
- **Operations**: Matrix multiplication and convolution
- **Performance**: 4x faster than CUDA cores for AI workloads
- **Programming**: Automatic optimization in frameworks like TensorFlow/PyTorch

---

# Performance Optimization Guidelines

## 1. Maximize Parallelism
- **Thread Count**: Ensure sufficient threads to hide memory latency
- **Block Size**: Choose optimal thread block dimensions for your hardware
- **Grid Size**: Scale across multiple SMs effectively

## 2. Optimize Memory Throughput
- **Coalesced Access**: Threads should access consecutive memory locations
- **Shared Memory**: Use shared memory for frequently accessed data
- **Memory Alignment**: Ensure proper data alignment for optimal bandwidth

## 3. Maximize Instruction Throughput
- **Warp Efficiency**: Minimize warp divergence
- **Instruction Mix**: Balance different types of operations
- **Occupancy**: Maximize active warps per SM

## 4. Minimize Memory Thrashing
- **Cache Locality**: Reuse data in cache when possible
- **Memory Access Patterns**: Design algorithms for GPU memory hierarchy
- **Data Movement**: Minimize host-device transfers

---

# Practical Considerations

## When to Use GPUs
- **Data-Parallel Workloads**: Same operation on large datasets
- **High Arithmetic Intensity**: Computation-heavy applications
- **Large Memory Bandwidth Requirements**: Data-intensive operations

## When Not to Use GPUs
- **Serial Algorithms**: Sequential dependencies limit parallelism
- **Small Datasets**: Overhead exceeds benefits
- **Frequent Host-Device Communication**: Memory transfer overhead

---

# References

- [GPU Architecture Fundamentals](https://faculty.iiit.ac.in/~kkishore/GPUArchitecture.pdf)
- [NVIDIA Deep Learning Performance Guide](https://docs.nvidia.com/deeplearning/performance/dl-performance-gpu-background/index.html)
- [GPU vs CPU Architecture Discussion](https://www.zhihu.com/question/22219245/answer/380597834)
- [NVIDIA Turing Architecture Deep Dive](https://developer.nvidia.com/blog/nvidia-turing-architecture-in-depth/)
- [CUDA Memory Statistics and Cache Analysis](https://docs.nvidia.com/gameworks/content/developertools/desktop/analysis/report/cudaexperiments/kernellevel/memorystatisticscaches.htm)
- [Understanding GPU Caches](https://www.rastergrid.com/blog/gpu-tech/2021/01/understanding-gpu-caches/)
- [CUDA SIMT Architecture](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#simt-architecture)
- [CUDA Device Memory Access](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#device-memory-accesses)
- [CUDA Shared Memory](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#shared-memory-5-x)