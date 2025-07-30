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

# Black–Scholes PDE 推导
我们希望构建一个投资组合，把价格的随机波动项给去除，只留下确定性的趋势

假设这个投资组合为：
* +1 单位的期权（价格为 V）
* -x 单位的股票（价格为 -xS）
那么投资组合的价格为
$$
    PV = V -xS
$$

# Black–Scholes期权定价公式
$$
    
$$

# 总结
Black-Scholes 的核心思想是：
* 构造一个无风险组合；
* 利用伊藤引理对资产价格进行建模；
* 通过无套利假设，导出偏微分方程；
* 最后通过求解 PDE，得到欧式期权的定价公式。

# Appendix
## 为什么欧式看涨期权 $C(S,t)$ 是股票价格 $S$ 的二阶连续可微函数