---
layout:     post
title:      "CUDA SIMT"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 计算机架构
    - CPU
    - 内存
---

# Streaming Multiprocessors (SMs)

# SIMT(Single-Instruction, Multiple-Thread)架构
Warp，基本单元，由SM创建、管理、调度和执行。Warp由32个Thread组成，每个Thread有独立的寄存器、算术逻辑单元(ALU)。一个Warp只有一个程序计数器。

一个Warp在某个时刻只能执行一个指令，因此不同分支的Threads的指令只能串行执行，处于当前分支的Threads正常执行指令，处于其它分支的Threads则会暂停。

# SMID(Single-Instruction, Multiple-Data)