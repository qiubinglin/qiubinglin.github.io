---
layout:     post
title:      "GPU Architecture"
date:       2024-05-09 16:25:00
author:     "Bing"
catalog:    true
tags:
    - GPU
    - CUDA
---

![](/img/post/Cpu-gpu.svg.png "CPU vs GPU")
Thousand of cheap workers are better than one expensive all-rounder.

# SIMT
SIMT(single instruction, multiple threads) is the combination of SIMD and multithreading. Threads in the same warp always handle same instructions.

# Architecture
![](/img/post/GPU-Hardware.jpg)

## Common components in processing unit

## Core abstraction
![](/img/post/simple_gpu_arch.png)

## SMs
![](/img/post/GPU-SM.jpg)

## Warp
![](/img/post/warp-divergence-example.png)

## Memory access
![](/img/post/gpu-warp-memory-access1.png)

![](/img/post/gpu-warp-memory-access2.png)

### Latency

## Threads switch

## CUDA cores vs Tensor cores
CUDA cores are designed to handle general-purpose computations in parallel.

Tensor cores are specially designed to handle deep learning operations.

# Performance guidelines
1. Maximize the parallelism of the algorithm.
2. Maximize data bandwith.
3. Maximize instruction bandwith.
4. Minimize memory thrashing.

# References
[https://faculty.iiit.ac.in/~kkishore/GPUArchitecture.pdf](https://faculty.iiit.ac.in/~kkishore/GPUArchitecture.pdf)

[https://docs.nvidia.com/deeplearning/performance/dl-performance-gpu-background/index.html](https://docs.nvidia.com/deeplearning/performance/dl-performance-gpu-background/index.html)

[https://www.zhihu.com/question/22219245/answer/380597834](https://www.zhihu.com/question/22219245/answer/380597834)