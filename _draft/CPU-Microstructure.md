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
```
Fetch -> Decode -> Rename -> Dispatch -> Execute -> Forwarding -> Write back -> Commit
```

### Fetch
* 从指令缓存（I-Cache）中根据 PC（程序计数器）取出指令
* 同时进行分支预测，预判下一条指令的地址，以提升流水线效率
* 在超标量处理器中，可能一次 fetch 多条指令（称为“instruction bundle”）

### Decode
* 将机器指令翻译成微操作（uops），提取出操作数、操作类型、目标寄存器等信息
* 同时进行依赖分析，初步构建指令之间的依赖图
* 复杂指令（如 x86 的某些指令）可能会被拆分为多个 uop

### Rename
* 解决 写后写（WAW） 和 读后写（RAW） 等数据依赖冲突
* 将逻辑寄存器映射到物理寄存器，打破名字依赖，实现乱序执行的前提
* 重命名表（Register Alias Table, RAT）是关键的数据结构

### Dispatch
* 将指令（uop）分发到对应功能单元的等待队列（Issue Queue）
* 检查指令是否可以进入调度窗口（通常有容量限制）

### Execute
* 指令实际在功能单元中执行，如 ALU、乘法器、分支判断器等
* 操作数来自物理寄存器文件或 Forwarding 网络
* 某些指令（如 memory load/store）在这一步只是发起地址计算

### Forwarding
* 这是一个辅助阶段，也可视为 Execution 内部机制的一部分
* 结果直接从执行单元输出，绕过物理寄存器，转发给等待该结果的后续指令，以减少等待周期（消除 RAW hazard）

### Write back
* 执行结果写入物理寄存器文件中
* 同时更新“重命名表”，以便后续使用
* 这并不会立刻提交结果到架构状态，仅对物理状态生效

### Commit
* 指令顺序提交，更新架构状态（如通用寄存器文件）
* 若有异常（如缺页、非法指令），此阶段会触发处理机制，撤销未提交指令
* 利用 Reorder Buffer（ROB）来保持提交的程序顺序一致性（即使之前乱序执行）

# Some Concepts
## Frontend and Backend
现代 CPU 的流水线结构可以大致分为 Frontend（前端） 和 Backend（后端） 两部分：
* Frontend: [Fetch, Decode]
* Backend: [Rename, Dispatch, Execute, Forwarding, Write back, Commit]

## Core and Uncore

# Core
## Frontend
### FTQ (Fetch Target Queue)
FTQ 是前端流水线的缓冲器，缓存的是 “我要从哪里取指令” 的信息，而不是指令本身

### Decoder

### IB (Issue Buffer)
Issue Buffer 是用于暂存和调度待执行指令的硬件结构，等待操作数准备就绪后发射到功能单元执行。它是支持乱序执行的关键组件。

### BPU (Branch Prediction Unit)
预测分支指令跳转方向与目标地址的模块
#### BTB (Branch Target Buffer)
存储预测分支的目标地址（跳到哪）
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

## INTC (Interrupt Controller)
Include local and external

## IMSIC (Incoming Message Signaled Interrupt Controller)
One IMSIC per core

## APLIC (Advanced Platform-Level Interrupt Controller)
外部中断控制器

## CLINT (Core Local Interruptor)
一个具体的INTC的硬件实现，它支持两种类型的中断：
* Timer interrupt
* Software interrupt (IPI)

## PCIe (Peripheral Component Interconnect Express)

# Appendix
## Strong Memory Model
一个线程所做的内存读写操作，在程序中出现的顺序，对其他线程看起来也是按照这个顺序发生的。

## Superscalar CPU
* 超标量处理器能在每个时钟周期中发射多条指令到不同的执行单元中
* 这些指令之间要满足独立性（没有依赖冲突），由硬件进行调度