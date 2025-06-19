---
layout:     post
title:      "CPU Microstructure"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - CPU
---

# Pipeline
## Five-stage pipeline
```
Instruction Fetch -> Instruction Decode -> Execute -> Memory access -> Register write back
```

## More complex

# Core
## Frontend
### FTQ (Fetch Target Queue)
FTQ 是前端流水线的缓冲器，缓存的是 “我要从哪里取指令” 的信息，而不是指令本身

### BPU (Branch Prediction Unit)
预测分支指令跳转方向与目标地址的模块
#### BTB (Branch Target Buffer)
用来预测分支的目标地址（跳到哪）
* In-Cache BTB 是一种将分支跳转信息集成到指令缓存中的优化设计，能够更快、更节省硬件地进行跳转预测，适合对性能和能效有高要求的现代 CPU
* L1 BTB (Level 1 Branch Target Buffer) L1 BTB 是 CPU 分支预测器中最靠近取指阶段的、延迟最低的 BTB，负责快速预测最近/常见的分支跳转目标地址

#### BIM (Branch History Table)
用来预测是否跳转（跳还是不跳）
#### RAS (Return Address Stack)
用来预测函数返回地址（ret 指令）

### TLB (Translation Lookaside Buffer)
地址转换缓存，它用来加速虚拟地址到物理地址的转换。
* ITLB (Instruction TLB)
* DTLB (Data TLB)

### Rename Unit
将程序中使用的“架构寄存器名（如 x1, x2）”映射成唯一的物理寄存器名（如 p34, p56），以避免因寄存器名冲突导致的假依赖（false dependency）

### Dispatch Unit
将已经重命名（Rename）的指令发送到对应的 Issue Queue（发射队列）中，等待执行

### Issue buffer
暂存已经解码并重命名的指令，等待操作数准备好后发射（Issue）给执行单元（EXU）执行

## Backend
### ALU

### Reorder buffer
追踪乱序执行的每条指令，并在结果就绪后，以程序顺序提交（commit）指令的执行结果，以实现乱序执行但顺序提交的架构一致性

## Vector
### VLSU

## LSU (Load store unit)
处理内存访问指令的硬件单元

## MMU (Memory Management Unit)
负责虚拟地址到物理地址转换（Address Translation）和内存保护的硬件单元

# Uncore
## NOC (Network on chip)

## Cache
### ICache
### DCache

### L1 Cache

### L2 Cache

### L3 Cache

### Cache coherence protocol
Necessary condition:
1. 写传播（Write Propagation）一个核心的写操作必须最终被其他核心看到
2. 写串行化（Write Serialization）所有核心对同一地址的写操作必须有全局一致的顺序（如CPU1写A=1，CPU2写A=2，所有核心必须按相同顺序观察到这些写操作）
3. 原子性（Atomicity）单个核心的读写操作不能被拆分（如读到的值不能是“半新半旧”）

## System
### IMSIC (Incoming Message Signaled Interrupt Controller)
One IMSIC per core

### APLIC (Advanced Platform-Level Interrupt Controller)

### PCIe (Peripheral Component Interconnect Express)

# Strong Memory Model
一个线程所做的内存读写操作，在程序中出现的顺序，对其他线程看起来也是按照这个顺序发生的。