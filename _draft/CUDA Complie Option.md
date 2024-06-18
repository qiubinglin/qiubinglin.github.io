---
layout:     post
title:      "CUDA Complie Option"
date:       2024-05-02 10:52:00
author:     "Bing"
catalog:    true
tags:
    - HPC
    - CUDA
---

# Options
## Option `--fmad`
This option enables (disables) the contraction of floating-point multiplies and adds/subtracts into floating-point multiply-add operations (FMAD, FFMA, or DFMA).

## Option `--ftz`
Control single-precision denormals support.

`--ftz=true` flushes denormal values to zero and `--ftz=false` preserves denormal values.

## Option `--prec-div`
This option controls single-precision floating-point division and reciprocals.

`--prec-div=true` enables the IEEE round-to-nearest mode and `--prec-div=false` enables the fast approximation mode.

## Option `--prec-sqrt`
This option controls single-precision floating-point square root.

`--prec-sqrt=true` enables the IEEE round-to-nearest mode and `--prec-sqrt=false` enables the fast approximation mode.

## Option `--use_fast_math`
Make use of fast math library.

`--use_fast_math` implies `--ftz=true --prec-div=false --prec-sqrt=false --fmad=true`.

# References
[https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/#nvcc-command-options](https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/#nvcc-command-options)
