---
layout:     post
title:      "RDMA"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - CPU
    - HPC
---

# DMA (Direct Memory Access)
Direct Memory Access（DMA，直接内存访问）是一种提高数据传输效率的机制，它允许外设设备直接读写内存，绕过 CPU 的干预

## Flow
1. CPU 设置 DMA 控制器（指定源地址、目的地址、数据长度、方向等）。
2. DMA 控制器接管总线（通常是内存总线）。
3. 数据从外设传输到内存（或反向），不需要 CPU 参与。
4. 传输完成后产生中断，通知 CPU。

### 网络数据包接收全过程
1. 数据包进入网卡（PHY -> MAC）
2. DMA 把数据包写入内存（网卡到 ring buffer）
3. 内核中断/轮询 -> NAPI 调度
4. 协议栈处理（IP/TCP/...）并放入 socket 接收缓冲区
5. 用户进程调用 recv()/read() 拿到数据

# Remote Direct Memory Access (RDMA)
RDMA 允许一台计算机直接访问另一台计算机的内存，不经由对方的 CPU、操作系统或软件栈干预，实现超低延迟、高吞吐量、低CPU占用率的数据传输

普通 TCP 网络 I/O 的开销：
```
用户态 buffer --> 系统调用 --> 内核协议栈（TCP/IP） --> 网卡
（每次都要拷贝、上下文切换、协议栈处理）
```

RDMA 的数据路径：
```
用户态 buffer --> RDMA NIC（RNIC） --> 网络 --> 对端内存
（绕过内核、绕过远端 CPU，不需要远端应用处理）
```

## 核心机制组成
1. Zero-copy 数据传输
* 用户态数据直接通过网卡 DMA 到对端内存
* 无需拷贝到内核空间、无需系统调用
* 零拷贝是 RDMA 性能的基础
2. Bypass 操作系统
* 一旦连接建立，通信双方无需系统调用
* 完全在用户态完成发送、接收
* 网卡（RNIC）执行协议栈逻辑（如 Infiniband/RoCE/iWARP）
3. 内存注册（Memory Registration）
* 通信前需要将本地/远端内存 注册到 RNIC，即：锁页，防止换出；建立物理地址映射；分配 memory region（MR），形成 rkey（remote key）授权。
4. Queue Pair（QP）通信通道
* 每个 RDMA 通信连接由一对 queue 构成：Send Queue (SQ)，Receive Queue (RQ)
* 应用将发送/接收请求放入 QP，由 RNIC 执行