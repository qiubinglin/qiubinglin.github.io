---
layout:     post
title:      "Fast Marching Method-快速行进方法"
subtitle:   "隐去曲面演变的时间项"
date:       2022-10-16 09:59:00
author:     "Bing"
catalog: true
tags:
    - 数值计算
    - 曲面演变
    - Fast Marching Method
    - 图算法
    - Dijkstra algorithm
    - Eikonal equation
---

# Eikonal equation
对于方程
$$
    \frac{\partial \varphi}{\partial t} + \vec{v} \cdot \triangledown \varphi = 0
$$
所描述的曲面演变过程，若曲面只经过每一个空间点一次，即存在函数 $T(\vec{x})$，那么Level Set方程可以简化为
$$
    \frac{\partial (T(\vec{x}) - t)}{\partial t} + \vec{v} \cdot \triangledown (T(\vec{x}) - t) = 0
$$
$$
    |\triangledown T(\vec{x})| = \frac{1}{v}
$$
其中 $v$ 是 $T(\vec{x})$ 梯度方向的投影值，此方程称为Eikonal equation，可以通过Fast Marching Method求解。

# Fast Marching Method-快速行进方法
1、初始化 $T(\vec{x})$：将已知 $T$ 的值的点标注为Alive，邻近Alive点的标注为Close，其余的标注为Far。根据Alive点计算出所有Close点的值。

2、开始循环：从Close集合中选出 $T$ 值最小的点，并将其标注成Trial。

3、将Trial点邻近的所有非Alive点标注为Close，并重新计算这些点的 $T$。

4、将Trial点标注为Alive。

5、回到2继续下一次循环，直至所有点均标注成Alive。

![](/img/post/Schematic-illustration-of-fast-marching-method-1-Finding-the-point-with-the-minimum.png)