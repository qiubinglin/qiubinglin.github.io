---
layout:     post
title:      "Address Translation in MMU"
date:       2025-09-08 22:30:00
author:     "Bing"
catalog:    true
tags:
    - CPU
---

# 如何通过页表转换地址
![alt text](/img/post/Address-Translation.png)

# 页表结构
虚拟内存本身是稀疏空间，在现代系统（如 RISC-V Sv39）中，虚拟地址是 39 位，总共 512GB 空间。但实际上：
* 只使用很小一部分，如几个 MB ~ GB
* 各段（代码段、栈、堆、mmap 区等）之间存在大范围空洞

因此页表的结构是多级树状结构，以 RISC-V Sv39 为例，虚拟地址是这样拆分的：
```
VA[38:0] → VPN[2], VPN[1], VPN[0], PageOffset[11:0]
```
* 每级页表是 512 项（即 9-bit 索引）
* 页表是一棵三层树：
```
root_page_table (512 entries)
 └──-> L1 page table (on demand)
     └──-> L2 page table (on demand)
         └──-> leaf PTE → physical page
```

## 页表项(PTE)

页表项(Page Table Entry, PTE)是页表中的基本单元，包含虚拟页到物理页的映射信息。在RISC-V Sv39中，PTE是64位结构：

```
63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32
|  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |
31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1  0
|  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |  Reserved  |
```

关键字段说明：
- **PPN[2:0]**: 物理页号，共44位，指向物理内存中的页
- **RSW**: 保留字段，供软件使用
- **D**: Dirty位，表示页是否被修改过
- **A**: Accessed位，表示页是否被访问过
- **G**: Global位，表示全局页（所有地址空间共享）
- **U**: User位，表示用户态可访问
- **X**: Execute位，表示可执行
- **W**: Write位，表示可写
- **R**: Read位，表示可读
- **V**: Valid位，表示PTE是否有效

## 地址转换过程

MMU的地址转换过程如下：

1. **提取虚拟页号(VPN)**: 从虚拟地址中提取VPN[2], VPN[1], VPN[0]
2. **多级页表查找**:
   - 使用VPN[2]作为根页表索引
   - 使用VPN[1]作为L1页表索引  
   - 使用VPN[0]作为L2页表索引
3. **检查权限**: 验证访问权限(R/W/X)和特权级别
4. **生成物理地址**: 将物理页号(PPN)与页偏移量组合

```
虚拟地址: 0x1234567890
分解为: VPN[2]=0x24, VPN[1]=0x68, VPN[0]=0xAC, Offset=0x890
```

# TLB (Translation Lookaside Buffer)

TLB是MMU中的高速缓存，用于加速地址转换过程。

## TLB的作用

- **缓存页表项**: 存储最近使用的虚拟页到物理页的映射
- **减少内存访问**: 避免每次地址转换都访问多级页表
- **提高性能**: 典型的TLB命中时间在1-2个时钟周期

## TLB结构

TLB通常采用全相联或组相联结构：

```
TLB Entry:
- Tag: 虚拟页号(VPN)
- Data: 物理页号(PPN) + 权限位
- Valid: 有效位
- ASID: 地址空间标识符(可选)
```

## TLB管理

### TLB Miss处理

当TLB未命中时，需要从页表中加载映射：

1. **硬件处理**: 现代CPU通常有硬件TLB miss处理器
2. **软件处理**: 某些架构需要软件处理TLB miss异常
3. **页表遍历**: 从根页表开始逐级查找

### TLB刷新

TLB刷新发生在以下情况：
- **进程切换**: 不同进程的地址空间映射不同
- **页表更新**: 修改页表后需要刷新相关TLB项
- **权限变更**: 修改页权限后需要刷新

## MMU性能优化

### 大页支持

现代MMU支持多种页大小：
- **4KB**: 标准页大小
- **2MB**: 大页，减少TLB miss
- **1GB**: 超大页，进一步减少TLB压力

### 预取机制

- **TLB预取**: 预测性加载TLB项
- **页表预取**: 预取下一级页表
- **分支预测**: 预测地址转换路径

## 异常处理

MMU可能产生以下异常：

### 页错误(Page Fault)

- **缺页异常**: 页不在内存中
- **权限异常**: 访问权限不足
- **保护异常**: 违反内存保护规则

### 地址错误

- **对齐错误**: 地址未按页边界对齐
- **范围错误**: 地址超出有效范围

## 实际应用考虑

### 内存管理

- **页回收**: 定期回收未使用的页
- **页交换**: 将不活跃页交换到磁盘
- **内存压缩**: 压缩内存以节省空间

### 安全考虑

- **ASLR**: 地址空间布局随机化
- **NX位**: 禁止执行位防止代码注入
- **SMEP/SMAP**: 防止内核执行用户代码
