---
layout:     post
title:      "Krylov-完全正交方法(FOM)和广义极小残差(GMRES)"
date:       2022-12-13 13:24:00
author:     "Bing"
catalog:    true
tags:
    - 数值计算
    - 矩阵计算
    - 最小二乘
    - 迭代方法
    - Krylov
---
一些定义参见[Krylov子空间方法](https://qiubinglin.github.io/2022/12/12/Krylov-subspace-method/)

# 完全正交方法(FOM)
在FOM中，选择约束空间 $L = K_m$，即
$$
    寻找 \overline{x} \in x^{(0)} + K_m，满足 b - A\overline{x} \bot K_m
$$
由 $\overline{x} \in x^{(0)} + K_m$ 可知，存在向量 $y \in R^m$ 使得
$$
    \overline{x} = x^{(0)} + V_m y
$$
另外根据正交性条件 $b - A\overline{x} \bot K_m$，有
$$
    V_m^T(b - A\overline{x}) = 0
$$

由Arnoldi过程性质，有
$$
    V_m^TAV_m = H_m
    \\
    V_m^T r_0 = V_m^T \beta v_1 = \beta e_1
$$
其中 $r_0 = b - Ax^{(0)}, \beta = ||r_0||_2, e_1 = [1,0,...0] \in R^m$。
则
$$
    0 = V_m^T(b - A\overline{x}) = \beta e_1 - H_m y
$$
如果 $H_m$ 非奇异，则
$$
    y = \beta H_m^{-1} e_1
$$

# 广义极小残差(GMRES)
在GMRES中，选择约束空间 $L = AK_m$，即
$$
    寻找 \overline{x} \in x^{(0)} + K_m，满足 b - A\overline{x} \bot AK_m
$$