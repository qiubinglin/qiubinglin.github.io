---
layout:     post
title:      "APLIC"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - CPU
---
APLIC(Advanced Platform-Level Interrupt Controller) 的主要功能是：
1. 管理平台中断源（例如外设的中断）。
2. 将中断路由到目标 hart（CPU核）或其 IMSIC。
3. 支持中断的虚拟化与客体（guest）路由。
4. 支持消息信号中断（MSI）发送给 IMSIC。

APLIC 是 PLIC（Platform-Level Interrupt Controller）在支持 AIA 体系下的升级方案，解决了 PLIC 不支持中断虚拟化、不适合多核调度的问题。

# APLIC的核心寄存器
| Register | Address offset | Feature |
|-----|-----|-----|
| DOMAINCFG | 0x0000 | 域配置，包括是否启用中断控制 |
| SOURCECFG[i] | 0x0010+i×4 | 每个中断源的配置（类型、目标等） |
| SETIP[i] | 0x2000+i×4 | 设置中断为待处理中（pending） |
| CLRIP[i] | 0x2800+i×4 | 清除中断的 pending 状态 |
| GENMSI | 0x1BC8 | 向 IMSIC 发送中断消息（MSI），指定中断源号 |
| MMSICFGADDR[i] / SMSICFGADDR[i] |  | 指定目标 IMSIC 地址 |
| MMSICFGDATA[i] / SMSICFGDATA[i] |  | 指定发送 MSI 的数据内容 |

## SOURCECFG[i]
该寄存器为中断源号 i 指定：
* 中断模式（edge/level triggered）
* 中断送往的目标 hart
* 中断是物理模式还是代理模式

# APLIC 的中断流程（从外设中断到 hart 处理）
我们以中断源通过 APLIC 触发中断，最终到 IMSIC 的流程为例说明。
1. 外设通过中断线（可能是 GPIO、PCIe、UART 等）发出信号，APLIC 的硬件逻辑检测到这个物理中断事件，根据映射为一个中断源号 i（根据DTB文件？）。
2. APLIC 硬件会将这个中断源 i 的 pending 状态置位，即设置 SETIP[i] = 1。
3. APLIC 检查中断域是否启用，以及是否处于 MSI 模式。
4. APLIC 根据中断源 i 的配置，向目标 hart 的 IMSIC 发送 MSI。所使用的 MSI 地址与数据在如下寄存器中设置：
   * MMSICFGADDR[i]（Machine 模式）或 SMSICFGADDR[i]（Supervisor 模式）设置发送给 IMSIC 的 物理地址。
   * MMSICFGDATA[i] / SMSICFGDATA[i] 设置发送给 IMSIC 的 数据值（通常是中断号）。
5. 一旦 APLIC 检测到中断 pending 并满足上述条件，它会主动发起 MSI 传输。这一步是自动的，但你也可以通过写 GENMSI 强制发送：
   * GENMSI（偏移固定：如 0x1BC8）软件可以向此寄存器写中断源号 i，以“立刻”发送该中断源的 MSI，通常用于同步屏障。

# Interact with IMSIC

# Appendix
## /proc/interrupts
