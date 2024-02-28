---
layout:     post
title:      "Fourier Transform"
date:       2024-02-17 15:03:00
author:     "Bing"
catalog:    true
tags:
    - 数值分析
    - 信号与系统
---

# 傅里叶级数
## 三角函数形式
对于周期 $T > 0$ 的周期函数 $f(t)$，有
$$
    f(t) = A_0 + \sum_{k=1}^{\infty}(A_k cos k \omega_T t + B_k sin k \omega_T t)
$$
其中 $\omega_T = 2\pi/T$，傅里叶系数
$$
    A_0 = \frac{1}{T} \int_{T} f(t) dt
$$
$$
    A_k = \frac{2}{T} \int_{T} f(t) cos k \omega_T t dt
$$
$$
    B_k = \frac{2}{T} \int_{T} f(t) sin k \omega_T t dt
$$

$f(t)$ 的 $N$ 阶近似 $f_N(t)$
$$
    f_N(t) = A_0 + \sum_{k=1}^{N}(A_k cos k \omega_T t + B_k sin k \omega_T t)
$$

## 振幅-相位形式
令 $A_k = D_k cos \varphi_k$，$B_k = D_k sin \varphi_k$，即 $D_k^2 = A_k^2 + B_k^2$，得到振幅-相位形式的傅里叶级数
$$
    f(t) = D_0 + \sum_{k=1}^{\infty} D_k cos(k \omega_T t - \varphi_k)
$$

## 指数形式
令
$$
    C_k = \begin{cases}
        A_0, k = 0 \\
        \frac{D_k}{2} e^{-i \varphi}, k > 0 \\
        C_{|k|}^*, k < 0
    \end{cases}
$$
得到指数形式的傅里叶级数
$$
    f(t) = \sum_{k=-\infty}^{\infty} C_k e^{ik \omega_T t}
$$
傅里叶系数
$$
    C_k = \frac{1}{T} \int_{T} f(t) e^{-ik \omega_T t} dt
$$

# 傅里叶变换
显然对于周期 $T > 0$ 的周期函数 $f(t)$
$$
    f(t) = \sum_{k=-\infty}^{\infty} C_k e^{ik \omega_T t}
    \\
    = \frac{1}{T} \sum_{k=-\infty}^{\infty} \int_{T} f(t) e^{-ik \omega_T t} dt e^{ik \omega_T t}
    \\
    = \frac{1}{T} \sum_{k=-\infty}^{\infty} F(\omega) e^{i \omega t}
$$
其中 $\omega = k\omega_T$，令 $T \to \infty$，黎曼和趋向于黎曼积分
$$
    f(t) = \frac{1}{2 \pi} \int_{-\infty}^{\infty} F(\omega) e^{i \omega t} d \omega
$$

***傅里叶变换***
$$
    F(\omega) = \int_{T} f(t) e^{-i \omega t} dt = \int_{-\infty}^{\infty} f(t) e^{-i \omega t} dt
$$

***傅里叶逆变换***
$$
    f(t) = \frac{1}{2 \pi} \int_{-\infty}^{\infty} F(\omega) e^{i \omega t} d \omega
$$

# 离散傅里叶变换(DFT)
给定函数 $f(t)$ ，其中 $x \in (-\infty, \infty)$，有 $N$ 个等间距采样点 $t_0,t_1...t_{N-1}$，$\Delta t = t_{m+1} - t_m$，那么傅里叶变换可以近似成
$$
    F(\omega) = \Delta t \sum_{k=0}^{N-1} f(t_k) e^{-i \omega t_m}
$$

取
$$
    \omega_n = \frac{2\pi n}{N\Delta t}, n \in [0, N-1]
$$
那么
$$
    F(\omega_n) = \Delta t \sum_{k=0}^{N-1} f(t_k) e^{-i \frac{2\pi n}{N\Delta t} (t_0 + k\Delta t)}
    \\
    = \Delta t e^{-i \frac{2\pi n}{N\Delta t}} \sum_{k=0}^{N-1} f(t_k) e^{-i \frac{2\pi}{N} nk}
$$

综上

***离散傅里叶变换(DFT)***
$$
    F[n] = \sum_{k=0}^{N-1} f[k]e^{-i \frac{2\pi}{N} nk}
$$

DFT写成矩阵形式
$$
    \begin{pmatrix}
        F[0] \\
        F[1] \\
        F[2] \\
        .... \\
        F[N-1] \\
    \end{pmatrix} = \begin{pmatrix}
        1 & 1 & 1 & 1 & .... & 1 \\
        1 & W & W^2 & W^3 & .... & W^{N-1} \\
        1 & W^2 & W^4 & W^6 & .... & W^{2 (N-1)} \\
        1 & W^3 & W^6 & W^9 & .... & W^{3 (N-1)} \\
        .... & .... & .... & .... & .... & .... \\
        1 & W^{N-1} & W^{2 (N-1)} & W^{3 (N-1)} & .... & W^{(N-1)^2}
    \end{pmatrix} = \begin{pmatrix}
        f[0] \\
        f[1] \\
        f[2] \\
        .... \\
        f[N-1] \\
    \end{pmatrix}
$$

***离散傅里叶逆变换(IDFT)***
$$
    f[k] = \frac{1}{N} \sum_{n=0}^{N-1} F[n]e^{i \frac{2\pi}{N} nk}
$$