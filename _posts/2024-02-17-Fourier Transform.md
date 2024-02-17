---
layout:     post
title:      "Fourier Transform"
date:       2024-02-17 15:03:00
author:     "Bing"
catalog:    true
tags:
    - 应用数学
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
    F(\omega) = \int_{T} f(t) e^{-i \omega t} dt
$$

***傅里叶逆变换***
$$
    f(t) = \frac{1}{2 \pi} \int_{-\infty}^{\infty} F(\omega) e^{i \omega t} d \omega
$$

# 离散傅里叶变换(DFT)
设 $f(t)$ 在 $[0, (N-1)T]$ 内有 $N$ 个等间距采样点 $f[0],f[1]...f[N-1]$，$f[k] = f(t_k)$，则 $f(t)$ 可以看成
$$
    f(t) = f(t) \sum_{k=0}^{N-1} \delta(t - t_k)
$$

傅里叶变换
$$
    F(\omega) = \int_{0}^{(N-1)T} f(t) e^{-i \omega t} dt
    \\
    = f[0]e^{-i0} + f[1]e^{-i \omega T} + ... + f[N-1]e^{-i \omega (N-1) T}
    \\
    = \sum_{k=0}^{N-1} f[k]e^{-i \omega k T}
$$

取
$$
    \omega = 0, \frac{2\pi}{NT}, \frac{2\pi}{NT} \times 2, ..., \frac{2\pi}{NT} \times (N-1)
$$

得到 ***离散傅里叶变换***
$$
    F[n] = \sum_{k=0}^{N-1} f[k]e^{-i \frac{2\pi}{N} nk}
$$

***离散傅里叶逆变换***
$$
    f[k] = \frac{1}{N} \sum_{n=0}^{N-1} F[n]e^{i \frac{2\pi}{N} nk}
$$