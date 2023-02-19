---
layout:     post
title:      "特征工程"
date:       2023-02-12 10:48:00
author:     "Bing"
catalog:    true
tags:
    - 数据分析
    - 特征工程
---

# 特征选择（Feature Selection）
通常来说，特征选择有以下几种方法。

1、**单变量特征选择**。通过单个特征变量与目标值的统计关系来选择特征。
```
selector_kbest = SelectKBest(f_regression, k=5)
X_kbest_train = selector_kbest.fit_transform(X_train, y_train)
X_kbest_test = selector_kbest.transform(X_test)

cols = X.columns

mask = selector_kbest.get_support()

selected_cols = cols[mask]

X_new = X[selected_cols]
print(X_new.columns)

#selectKbest model
xgb_kbest = xgb_train(X_kbest_train,X_kbest_test)
```

2、**递归特征剔除**。从选择所有的特征开始，不断地训练模型并剔除最不重要的特征。
```
# select 25 features
selector_rfe = RFE(LinearRegression(), n_features_to_select=25)
#fit transform
X_rfe_train = selector_rfe.fit_transform(X_train, y_train)
X_rfe_test = selector_rfe.transform(X_test)

selected_features_RFE = X.columns[selector_rfe.get_support()]
print("Selected Features:", selected_features_RFE)

#rfe_model
xgb_rfe = xgb_train(X_rfe_train,X_rfe_test)
```

3、**Lasso正则化**。该方法使用Lasso正则化来将不重要特征的系数收缩至零，最后将零系数的特征剔除。
```
selector_lassocv = LassoCV()
selector_lassocv.fit(X_train, y_train)
mask = selector_lassocv.coef_ != 0

# Get the column names of the selected features
selected_features_lasso = X.columns[mask]

X_lassocv_train = X_train.loc[:,mask]
X_lassocv_test = X_test.loc[:,mask]
print("Selected Features:", selected_features_lasso)

#lasso_cv model
xgb_lassocv = xgb_train(X_lassocv_train,X_lassocv_test)
```

4、**随机森林特征重要性**。根据随机森林模型的特征重要性属性来选择特征。
```
# initialize the selector
selector_rf = RandomForestRegressor()

# fit the selector to the data
selector_rf.fit(X_train, y_train)

# get the feature importances
imp = selector_rf.feature_importances_

# keep only the features with importance greater than 0.01

X_rf_train = X_train.loc[:,imp > 0.01]
X_rf_test = X_test.loc[:,imp > 0.01]

# get the column names of the selected features
selected_features_RF = X_rf_test.columns

print("Selected Features:", selected_features_RF)

# rf model
xgb_rf = xgb_train(X_rf_train,X_rf_test)
```