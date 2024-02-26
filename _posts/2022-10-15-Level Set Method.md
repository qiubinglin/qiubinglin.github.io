---
layout:     post
title:      "Level Set Method-水平集方法"
subtitle:   "描述曲面的演变"
date:       2022-10-15 17:11:00
author:     "Bing"
catalog: true
tags:
    - 数值分析
    - Level Set Method
---

# 曲面演变问题
置于速度场 $\vec{v}$ 中的曲面 $\varphi$，初始时刻下 $\varphi = \varphi_0$，那么曲面 $\phi$ 如何随着时间 $t$ 演变？

## 在高维中简化问题
![](/img/post/1920px-Level_set_method.png)

若把时间 $t$ 也看作描述曲面的一个维度，那么曲面可以表述为
$$
    \varphi(\vec{x},t) = 0
$$
对 $t$ 求导，由链式法则
$$
    \frac{\partial \varphi}{\partial t} + \vec{v} \cdot \triangledown \varphi = 0
$$
因此可以通过求解上述偏微分方程求得任意 $t$ 时刻曲面 $\varphi$ 的形貌。

$\varphi(\vec{x})$ 的选择存在一定的自由度，通常选用函数
$$
    \varphi(\vec{x}) = d
$$
其中 $d$ 是 $\vec{x}$ 到曲面的距离，通常规定曲面的内部为负，外部为正，因此又称为符号距离函数。

$\varphi$ 称为Level Set函数，对应 $\varphi = 0$ 曲面即是零水平集。这一求解曲面演变问题的方法即被称为Level Set Method-水平集方法。