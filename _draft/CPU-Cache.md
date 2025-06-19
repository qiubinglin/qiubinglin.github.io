---
layout:     post
title:      "CPU Cache"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - CPU
---

# Key Concepts
* Line offset
* Tag
* Index
  
## Background
Cache 被划分成很多个 Cache Block（或叫 Cache Line），每个 block 存储一段主存数据（比如 64 字节）。

这些 block 被划分为多个 组（Set），每组可以有多个块（称为 n 路组相联）。

例如：4 路组相联，表示每组可以容纳 4 个 block。

## Line offset
作用：确定你要访问的这个 block 内部的哪一个字节

每个 Cache Line 包含多个字节（如 64B）

如果 Line 大小是 64 字节 → 需要 6 bits 来表示偏移（2^6 = 64）

Line Offset 位数 = log₂(Line Size)

## Index
作用：决定这个地址应该映射到 Cache 中的哪一组（Set）

Cache 被划分为多个组，每个组包含若干个块（ways）

Index 从地址中提取出 组号

Index 位数 = log₂(Cache sets 数量)

## Tag
作用：为了确认这个地址是否真的存在于 Cache 中

因为多个地址可能映射到同一组，所以需要用 Tag 来区分

每个 Cache Line 都保存一个 Tag，如果地址的 Tag 匹配 → 命中，否则 → Miss

Tag = 剩下的高位地址部分


```
[ Tag bits ][ Index bits ][ Line Offset bits ]
```