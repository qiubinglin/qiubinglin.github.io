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

三层抽象

# Memory Hierarchy

## Register
线程独享内存。

## Local Memory
线程独享内存，对Global Memory的抽象。

## L2 Cache
L2 Cache可以缓存下需要经常使用的数据，相比直接从Global Memory中访问数据，它具有高带宽低延迟的访问优势。所有SMs共享。

## 共享内存(Shared Memory)
Shared Memory是一块可以被CUDA Block内所有线程访问的内存。对L1 Cache的抽象。

## Distributed Shared Memory
块集群(Thread Block Cluster)内共享的内存。

# 页锁定主内存(Page-Locked Host Memory)
CPU提供页锁定内存机制，GPU从页锁定内存中拷贝数据比一般内存要块。

## Portable Memory
多设备共用页锁定主内存。

## Write-Combining Memory

## Mapped Memory

## 内存同步

# CPU与GPU的内存交互

# 虚拟内存(Virtual memory)

# 固定内存(Pinned memory)

# 附录

## 直接内存访问(Direct memory access, DMA)