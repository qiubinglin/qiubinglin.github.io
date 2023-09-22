---
layout:     post
title:      "CUDA-内存模型"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 高性能计算
    - GPU
    - CUDA
---

# Memory Hierarchy

## Register and Local Memory
线程独享内存。

## L2 Cache
L2 Cache可以缓存下需要经常使用的数据，相比直接从Global Memory中访问数据，它具有高带宽低延迟的访问优势。

## 共享内存(Shared Memory)
Shared Memory是一块可以被CUDA Block内所有线程访问的内存。

## Distributed Shared Memory
块集群(Thread Block Cluster)内共享的内存。

# 页锁定主内存(Page-Locked Host Memory)
CPU提供页锁定内存机制，GPU从页锁定内存中拷贝数据比一般内存要块。

## Portable Memory
多设备共用页锁定主内存。

## Write-Combining Memory

## Mapped Memory

# CPU与GPU的内存交互

# 虚拟内存(Virtual memory)

# 固定内存(Pinned memory)

# 附录

## 直接内存访问(Direct memory access, DMA)