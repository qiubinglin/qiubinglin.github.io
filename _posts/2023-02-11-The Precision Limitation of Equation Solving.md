---
layout:     post
title:      "方程求解的精度极限"
date:       2023-02-11 16:16:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
---

# 前向误差与后向误差
***定义***
假设 $f$ 是一个函数，$r$ 是函数的根。对于根求解问题，假设 $x_a$ 是 $r$ 的近似值，那么近似 $x_a$ 的后向误差是 $|f(x_a) - f(r)|$，前向误差是 $|r - x_a|$。

# 函数的条件数
设函数 $f(x)$ 可导，$r^{*}$ 是 $r$ 的近似值，根据Taylor公式
$$
    f(r^*) - f(r) = f'(r)(r^* - r) + \frac{f''(\xi)}{2}(r^* - r)^2
$$
当 $r^* \approx r$ 时省略平方项。得
$$
    |\frac{f(r^*) - f(r)}{f(r)}| = |\frac{rf'(r)}{f(r)}| \times |\frac{r^* - r}{r}| 
$$
$C_p(r) \triangleq |\frac{rf'(r)}{f(r)}|$ 称为条件数。

# 根搜索的敏感性
## 根敏感公式
假设 $r$ 是函数 $f(x)$ 的根，并且 $r + \Delta r$ 是 $f(x) + \epsilon g(x)$ 的根，
$$
    f(r + \Delta r) + \epsilon g(r + \Delta r) = 0
$$
$$
    f(r) + f'(r) \Delta r + \epsilon g(r) + \epsilon g'(r) \Delta r + O((\Delta r)^2) = 0
$$
忽略 $O((\Delta r)^2)$ 高阶无穷小项，则当 $\epsilon \ll f'(x)$ 时
$$
    \Delta r = - \frac{\epsilon g(r)}{f'(r)}
$$
其中 $\epsilon$ 即是误差放大因子。

# 减小误差的方法
1. 避免相近数相减
2. 避免将绝对值较小的数作为分母（数量级相差较大时）
3. 加和时按照绝对值从小到大求和
4. 简化计算

# References
Timothy Sauer. Numerical Analysis. Chapter 1.

[https://math.ecnu.edu.cn/~jypan/Teaching/NA/slides_01C_Error.pdf](https://math.ecnu.edu.cn/~jypan/Teaching/NA/slides_01C_Error.pdf)