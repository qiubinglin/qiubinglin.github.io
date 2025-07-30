---
layout:     post
title:      "Black–Scholes模型-期权定价"
date:       2023-09-24 15:16:00
author:     "Bing"
catalog:    true
tags:
    - 金融数学
---

Black-Scholes 模型是一种用于定价欧式期权的数学模型。欧式期权是指只能在到期日执行的期权。

# 假设条件
Black-Scholes 模型基于以下假设：
1. 标的资产价格服从几何布朗运动（Geometric Brownian Motion）：
$$
    dS= \mu Sdt + \sigma SdW
$$
2. 无套利市场
3. 可以连续交易
4. 不存在交易费用和税收
5. 可以无风险借贷，利率为常数 $r$
6. 欧式期权，只能在到期日执行

# Black–Scholes期权定价公式
$$
    
$$

# Appendix
## 为什么欧式看涨期权 $C(S,t)$ 是股票价格 $S$ 的二阶连续可微函数