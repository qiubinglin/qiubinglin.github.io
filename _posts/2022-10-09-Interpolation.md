---
layout:     post
title:      "插值"
subtitle:   " \"关于插值的一点介绍\""
date:       2022-10-09 17:15:00
author:     "Bing"
catalog: true
tags:
    - 数值分析
    - 插值
---

# 插值的定义
插值，即使用插值函数去近似真实函数。多项式函数非常适用于计算机计算，因此插值函数通常选用多项式函数。其严格定义如下。

如果对于每一个 $1 \leq i \leq n$，$y_i = P(x_i)$，则称函数 $y = P(x)$ 插值数据点 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$。

# 拉格朗日插值
假设给定 $n$ 个数据点 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$，则
$$
    y = \sum_{i=1}^n { y_i \prod_{j=1,j \neq i}^n \frac{x - x_j}{x_i - x_j} }
$$
是这 $n$ 个点的拉格朗日插值多项式。

# 多项式插值主定理
令 $(x_1, y_1), (x_2, y_2)...(x_n, y_n)$ 是平面中的 $n$ 个点，具有不同的 $x_i$ 坐标，则存在一个且仅有一个 $n-1$ 次或者更低次的多项式 $P$ 满足 $y_i = P(x_i), i=1,2...n$。

证明。拉格朗日插值证明 $P$ 的存在性，代数基本定理结合反证法证明 $P$ 的唯一性。

# 牛顿差商
用 $f[x_1...x_n]$ 表示（唯一）多项式的 $x^{n-1}$ 项的系数，该多项式插值 $((x_1, f(x_1))... (x_n, f(x_n)))$。

牛顿差商公式
$$
    P(x) = f[x_1] + f[x_1 x_2](x - x_1) +...+ f[x_1...x_n](x - x_1)...(x - x_{n-1})
$$
显然通过递归带入 $x_1...x_k$ 可以计算出 $f[x_1...x_k]$。

定义如下差分等式
$$
    f[x_k] = f(x_k)
    \\
    f[x_k x_{k+1}] = \frac{f[x_{k+1}] - f[x_k]}{x_{k+1} - x_k}
    \\
    f[x_k...x_{k+n}] = \frac{f[x_{k+1}...x_{k+n}] - f[x_k...x_{k+n-1}]}{x_{k+n} - x_k}
$$
则有
$$
    f[x_1] = f(x_1)
$$
$$
    f[x_1...x_k] = \frac{f[x_2...x_k] - f[x_1...x_{k-1}]}{x_k - x_1}, (k > 1)
$$

# 样条插值（Spline Interpolation）
样条插值的基本思想是用多个低阶的插值多项式去拟合数据点（区分于用所有的数据点得到一个复杂的高阶多项式）。样条插值多用来平滑曲线。

## 三次样条
考虑数据点集 $(x_1, y_1)...(x_n, y_n)$，其中$x_1 < ... < x_n$。三次样条构建的插值多项式
$$
    S_1...S_{n-1}
$$

为$S_i(x_i) = y_i + b_i(x - x_i) + c_i(x - x_i)^2 + d_i(x - x_i)^3$

其定义域为 $[x_i, x_{i+1}]$。满足

***性质1***
$$
    S_i(x_i) = y_i, S_i(x_{i+1}) = y_i; i=1...n-1
$$

***性质2***
$$
    S_{i-1}'(x_i) = S_i'(x_i); i=2...n-1
$$

***性质3***
$$
    S_{i-1}''(x_i) = S_i''(x_i); i=2...n-1
$$

***性质4a***
$$
    S_1''(x_1) = 0, S_{n-1}''(x_n)=0
$$
显然由这4个性质可以得到 $3n-3$ 个约束条件解出所有的未知系数。

以下是使用MKL实现三次样条的例子
```
#include "mkl.h"

#define NX 100                     /* Size of partition, number of breakpoints */
#define NSITE 1000                 /* Number of interpolation sites */
#define SPLINE_ORDER DF_PP_CUBIC   /* A cubic spline to construct */

int main()
{
    int status;          /* Status of a Data Fitting operation */
    DFTaskPtr task;      /* Data Fitting operations are task based */

    /* Parameters describing the partition */
    MKL_INT nx;          /* The size of partition x */
    double x[NX];         /* Partition x */
    MKL_INT xhint;       /* Additional information about the structure of breakpoints */

    /* Parameters describing the function */
    MKL_INT ny;          /* Function dimension */
    double y[NX];         /* Function values at the breakpoints */
    MKL_INT yhint;       /* Additional information about the function */
    
    /* Parameters describing the spline */
    MKL_INT  s_order;    /* Spline order */
    MKL_INT  s_type;     /* Spline type */
    MKL_INT  ic_type;    /* Type of internal conditions */
    double* ic;         /* Array of internal conditions */
    MKL_INT  bc_type;    /* Type of boundary conditions */
    double* bc;         /* Array of boundary conditions */

    double scoeff[(NX-1)* SPLINE_ORDER];   /* Array of spline coefficients */
    MKL_INT scoeffhint;            /* Additional information about the coefficients */

    /* Parameters describing interpolation computations */
    MKL_INT nsite;        /* Number of interpolation sites */
    double site[NSITE];   /* Array of interpolation sites */
    MKL_INT sitehint;     /* Additional information about the structure of 
                             interpolation sites */

    MKL_INT ndorder, dorder;    /* Parameters defining the type of interpolation */

    double* datahint;   /* Additional information on partition and interpolation sites */

    double r[NSITE];    /* Array of interpolation results */
    MKL_INT rhint;     /* Additional information on the structure of the results */
    MKL_INT* cell;      /* Array of cell indices */

    /* Initialize the partition */
    nx = NX;

    /* Set values of partition x */
    ...
    xhint = DF_NON_UNIFORM_PARTITION;  /* The partition is non-uniform. */

    /* Initialize the function */
     ny = 1;               /* The function is scalar. */
     
    /* Set function values */
    ...
    yhint = DF_NO_HINT;    /* No additional information about the function is provided. */

    /* Create a Data Fitting task */
    status = dfdNewTask1D( &task, nx, x, xhint, ny, y, yhint );

    /* Check the Data Fitting operation status */
    ...

    /* Initialize spline parameters */
    s_order = DF_PP_CUBIC;     /* Spline is of the fourth order (cubic spline). */ 
    s_type = DF_PP_BESSEL;     /* Spline is of the Bessel cubic type. */ 

    /* Define internal conditions for cubic spline construction (none in this example) */
    ic_type = DF_NO_IC; 
    ic = NULL;

    /* Use not-a-knot boundary conditions. In this case, the is first and the last 
     interior breakpoints are inactive, no additional values are provided. */
    bc_type = DF_BC_NOT_A_KNOT; 
    bc = NULL;
    scoeffhint = DF_NO_HINT;    /* No additional information about the spline. */ 

    /* Set spline parameters  in the Data Fitting task */
    status = dfdEditPPSpline1D( task, s_order, s_type, bc_type, bc, ic_type,
                                ic, scoeff, scoeffhint );
    
    /* Check the Data Fitting operation status */
    ...

    /* Use a standard method to construct a cubic Bessel spline: */
    /* Pi(x) = ci,0 + ci,1(x - xi) + ci,2(x - xi)2 + ci,3(x - xi)3, */
    /* The library packs spline coefficients to array scoeff: */
    /* scoeff[4*i+0] = ci,0, scoef[4*i+1] = ci,1,         */   
    /* scoeff[4*i+2] = ci,2, scoef[4*i+1] = ci,3,         */   
    /* i=0,...,N-2  */
    status = dfdConstruct1D( task, DF_PP_SPLINE, DF_METHOD_STD );

    /* Check the Data Fitting operation status */
    ...

    /* Initialize interpolation parameters */
    nsite = NSITE;

    /* Set site values */
    ...

    sitehint = DF_NON_UNIFORM_PARTITION; /* Partition of sites is non-uniform */

    /* Request to compute spline values */
    ndorder = 1;
    dorder = 1;
    datahint = DF_NO_APRIORI_INFO;  /* No additional information about breakpoints or
                                       sites is provided. */
    rhint = DF_MATRIX_STORAGE_ROWS; /* The library packs interpolation results 
                                       in row-major format. */
    cell = NULL;                    /* Cell indices are not required. */

    /* Solve interpolation problem using the default method: compute the spline values
       at the points site(i), i=0,..., nsite-1 and place the results to array r */ 
    status = dfdInterpolate1D( task, DF_INTERP, DF_METHOD_STD, nsite, site,
    sitehint, ndorder, &dorder, datahint, r, rhint, cell );
 
    /* Check Data Fitting operation status */ 
     ...

    /* De-allocate Data Fitting task resources */
     status = dfDeleteTask( &task );
    /* Check Data Fitting operation status */ 
     ...
    return 0;
}
```

## 贝塞尔曲线
考虑两点 $X_1, X_2$，给出一阶贝塞尔曲线公式
$$
    X = (1 - k)X_1 + k X_2
$$
三点
$$
    
$$


# 插值误差
如果 $P(x)$ 是 $n - 1$ 阶或更低阶的插值多项式，拟合数据点 $(x_1, y_1)...(x_n, y_n)$。那么 $P(x)$ 的插值误差是
$$
    f(x) - P(x) = \frac{f^{(n)}(c)}{n!}(x - x_1)...(x - x_n)
$$
其中 $c$ 在最小和最大的 $n+1$ 个数字 $x, x_1...x_n$ 之间。

证明

$P_{n-1}(t)$ 是数据点 $(x_1, y_1)...(x_n, y_n)$ 的插值多项式，若新加入任意点 $(x, y)$，则
$$
    P_{n}(t) = P_{n-1}(t) + f[x_1...x_n, x](t - x_1)...(t - x_n)
$$
于是对于任意点 $x$ 有
$$
    f(x) = P_{n}(x) = P_{n-1}(x) + f[x_1...x_n, x](x - x_1)...(x - x_n)
$$
现在定义
$$
    h(t) = f(t) - P_{n-1}(t) - f[x_1...x_n, x](t - x_1)...(t - x_n)
$$
因为 $h(x) = h(x_1) =...= h(x_n) = 0$，根据罗尔定理函数 $h$ 在最小和最大的 $n+1$ 个数字 $x, x_1...x_n$ 之间存在 $n$ 个点满足 $h'=0$，以此类推此区间存在一个点 $c$ 满足
$$
h^{(n)}(c) = 0
$$
又因为
$$
    h^{(n)}(t) = f^{(n)}(t) - f[x_1...x_n, x](n!)
$$
则
$$
    f[x_1...x_n, x] = \frac{f^{(n)}(c)}{n!}
$$

# 龙格现象
在插值均匀分布的点集时，多项式在插值区间的端点附近扭动。因此，数据点选取对插值误差有很大的影响。

# 附录
## 代数基本定理
每个复系数 $n$ 次多项式 $p(x) = a_0 + a_1x +...+a_nx^n (a_n \neq 0)$ 有乘积表达式
$$
    p(x) = a_n(x - x_1)(x - x_2)...(x - x_n)
$$
其中复数 $x_1...x_n$ 除顺序外是唯一确定的。

## 罗尔定理
如果函数 $f$ 在 $[a, b]$ 上连续，$(a, b)$ 上可导，且 $f(a) = f(b)$，那么 $(a, b)$ 上存在一点 $\xi(a < \xi < b)$ 使得 $f'(\xi) = 0$。