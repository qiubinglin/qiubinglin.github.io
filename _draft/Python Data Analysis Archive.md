---
layout:     post
title:      "Python数据分析归档"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 数据分析
    - Python
---

# pandas
## 计算 DataFrame 中数值列的基本统计量
```
DataFrame.describe()
```

## 剔除数据
```
# Drop column data inplace, drop 'id' column
train_df.drop(columns=['id'], inplace=True)
```

# matplotlib
## 创建figure和一系列的subplots
```
nrows, ncols = 1, 1
fig, ax = plt.subplots(nrows, ncols)
```

## matplotlib.figure绘图元素持有者

## matplotlib.axes绘图数据持有者
管理绘图数据、坐标信息、标题等，用户主要使用该对象来作图。
