---
layout:     post
title:      "GPU Architecture"
date:       2024-03-17 16:25:00
author:     "Bing"
catalog:    true
tags:
    - GPU
    - CUDA
---

![](/img/post/gpu-devotes-more-transistors-to-data-processing.png "CPU vs GPU")

Thousand of cheap workers are better than one expensive all-rounder.

# SIMT
SIMT(single instruction, multiple threads) is the combination of SIMD and multithreading. 

# Architecture
![](/img/post/GPU-Hardware.jpg)

## Simple GPU Structure
![](/img/post/simple_gpu_arch.png)

Tasks are distributed to SMs. And then instructions and data are routed through DRAM, L2, L1 to SMs.

## SMs
![](/img/post/GPU-SM.jpg)

Components:
1. Arithmetic logic unit(ALU).
2. Floating point unit(FPU).
3. Special function unit(SFU).
4. LD/ST.
5. Register file.
6. Warp scheduler and Dispatch unit.
7. Tensor cores.
8. L1 cache.
9. Tex, designed to handles texture.
10. RT cores, designed to accelerates ray-traced graphics.

## Execution
At runtime, a thread block is placed on an SM for execution, enabling all threads in a thread block to communicate and synchronize efficiently.

![](/img/post/utilize-8sm-gpu.png)

## Warp
![](/img/post/warp-divergence-example.png)

The multiprocessor creates, manages, schedules, and executes threads in groups of 32 parallel threads called warps. Individual threads composing a warp start together at the same program address, but they have their own instruction address counter and register state and are therefore free to branch and execute independently.

Threads in the same warp always handle a same instruction at a time.

## Memory access
![](/img/post/gpu-warp-memory-access1.png)

![](/img/post/gpu-warp-memory-access2.png)

A warp can access 128 bytes of continuous and aligned memory, which equals $Warpsize \times 4$, at a time.

### Latency and Throughput
Compared to CPU, GPU has higher latency but higher throughput.

## Threads switch
Because of registers redundancy, GPU is able to switch threads by only swiching registers.

## CUDA cores vs Tensor cores
CUDA cores are designed to handle general-purpose computations in parallel.

Tensor cores are specially designed to handle deep learning operations.

# Performance guidelines
1. Maximize the parallelism of the algorithm.
2. Maximize memory throughput.
3. Maximize instruction throughput.
4. Minimize memory thrashing.

# References
[https://faculty.iiit.ac.in/~kkishore/GPUArchitecture.pdf](https://faculty.iiit.ac.in/~kkishore/GPUArchitecture.pdf)

[https://docs.nvidia.com/deeplearning/performance/dl-performance-gpu-background/index.html](https://docs.nvidia.com/deeplearning/performance/dl-performance-gpu-background/index.html)

[https://www.zhihu.com/question/22219245/answer/380597834](https://www.zhihu.com/question/22219245/answer/380597834)

[https://developer.nvidia.com/blog/nvidia-turing-architecture-in-depth/](https://developer.nvidia.com/blog/nvidia-turing-architecture-in-depth/)

[https://docs.nvidia.com/gameworks/content/developertools/desktop/analysis/report/cudaexperiments/kernellevel/memorystatisticscaches.htm](https://docs.nvidia.com/gameworks/content/developertools/desktop/analysis/report/cudaexperiments/kernellevel/memorystatisticscaches.htm)

[https://www.rastergrid.com/blog/gpu-tech/2021/01/understanding-gpu-caches/](https://www.rastergrid.com/blog/gpu-tech/2021/01/understanding-gpu-caches/)

[https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#simt-architecture](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#simt-architecture)