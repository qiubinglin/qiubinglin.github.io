---
layout:     post
title:      "Profiling"
date:       2024-05-09 16:25:00
author:     "Bing"
catalog:    true
tags:
    - Hardware
    - HPC
---

# Before Profiling
1. Choose the most suitable algorithm according to the computing capability of device.
2. Optimize the algorithm in time complexity and space complexity.

# 如何判断性能优化瓶颈
## 硬件瓶颈指南
|指标|理论极限|如何评估|
|-|-|-|
| CPU 利用率 | 100% 单核/多核 | `perf`, `top`, `htop` |
| 内存带宽 | 内存控制器最大带宽 | `pcm-memory`, `numastat` |
| L1/L2/L3 cache miss 率 | 尽量低 | `perf stat`, `cachegrind` |
| 分支预测命中率 | >95% 理想      | `perf stat -e branch-misses` |
| 网络 IO | 网卡带宽、包转发速率   | `ethtool`, `pktgen` |
| 存储 IO | SSD/HDD 理论带宽 | `fio`, `iostat` |


# Useful Tools
## [gprof](https://ftp.gnu.org/old-gnu/Manuals/gprof-2.9.1/html_mono/gprof.html)

Finding which part of a program are taking most of the execution time.

## [pstree](https://man7.org/linux/man-pages/man1/pstree.1.html)

## htop

## [perf](https://perf.wiki.kernel.org/index.php/Main_Page)