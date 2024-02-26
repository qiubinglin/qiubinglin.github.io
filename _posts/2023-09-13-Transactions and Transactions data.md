---
layout:     post
title:      "交易与交易数据"
date:       2023-09-13 17:30:00
author:     "Bing"
catalog:    true
tags:
    - 金融
---

# Limit order book(LOB)
限价委托簿(LOB)是一种记录买卖双方限价委托的清单，常用于金融市场。通过它可以很容易地看出市场的买卖需求和价格。

![](/img/post/limit-order-book.png "限价委托簿。当市场出现114.50价格150份的限价买单时，市场发生订单撮合，限价委托簿变化")

LOB的每一行(Level)由两部分组成：价格与数量。

LOB分为两方：卖方(Asks)、买方(Bids)

价差(Spread)：最优卖单与最优买单的价差。

中间价格(Mid Price)：(最优卖单价格 + 最优买单价格) / 2

最小报价单位(Tick size)：最小的价格变动单位。

## 市价单(Market Order)：
固定数量并以当前市场价格买卖的订单，会遭遇滑点。市价单减小市场流动性。

## 限价单(Limit Order)：
固定数量与价格的订单。限价单增大市场流动性。

## 流动性(Liquidity)
流动性好的市场价差小，订单量大。反之则流动性大。

# Roll's model of bid-ask bounce
Roll's model是一个经典的市场微观结构模型（基于有效市场假说）。在 $t_i$ 时刻，$Pri^*_i$ 为有效市场价格，$Pri_i$ 为交易价格，有
$$
    Pri_i = Pri^*_i + cI_i
$$
其中 $2c$ 为市场的买卖波动系数，买入(或卖出)时 $I_i = 1 (or -1)$。

并且有如下假设
$$
    P\{I_i = 1\} = P\{I_i = -1\} = 1 / 2
$$
设
$$
    D_i = Pri_i - Pri_{i-1} = Pri^*_i - Pri^*_{i-1} + c(I_i - I_{i-1})
$$
有
$$
    Cov(D_i, D_{i - j}) =
    \begin{cases}
        -c^2, j = 1 \\
        0, j >= 2
    \end{cases}
$$

# 有噪音的市场微观结构模型
令 $Y_{t_i} = log(Pri_i)$，$X_{t_i} = log(Pri^*_i)$，模型可以表示为
$$
    Y_{t_i} = X_{t_i} + \epsilon_i
$$
$$
    D_i = Y_{t_i} - Y_{t_{i-1}} \\
    Cov(D_i, D_{i - j}) =
    \begin{cases}
        -v_{\epsilon}, j = 1 \\
        0, j >= 2
    \end{cases}
$$

# 用几何布朗运动描述市场价格
考虑给标准布朗运动加上仅与时间相关的漂移项(drift) $\mu t$，以及一个尺度参数 $\sigma$，得到一个带漂移的布朗运动
$$
    X(t) = \mu t + \sigma B(t) \\
    dX(t) = \mu dt + \sigma dB(t)
$$
其中 $B(t)$ 是布朗运动。

但实际上 $\mu$ 和 $\sigma$ 是随时间变化的
$$
    dX(t) = \mu(t) dt + \sigma(t) dB(t)
$$

# 市场价格的波动性
## Realized Variance
市场价格的二次变差，经常用来描述市场的波动性。

# 交易数据
交易所交易记录的格式通常有两种。

1. Order-based Book
2. Level-based Book

# 附录
## 协方差
协方差用于衡量随机变量间的相关程度。对于两个实随机变量 $X$ 和 $Y$，它们的协方差为
$$
    Cov(X, Y) = E[(X - E[X]) (Y - E[Y])]
$$
利用[数学期望的线性特性](https://eng.libretexts.org/Bookshelves/Computer_Science/Programming_and_Computation_Fundamentals/Mathematics_for_Computer_Science_(Lehman_Leighton_and_Meyer)/04%3A_Probability/18%3A_Random_Variables/18.05%3A__Linearity_of_Expectation)，整理得
$$
    Cov(X, Y) = E[XY] - E[X]E[Y]
$$