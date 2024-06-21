---
layout:     post
title:      "Intrinsics Function"
date:       2024-05-02 10:52:00
author:     "Bing"
catalog:    true
tags:
    - HPC
---

In computer software, in compiler theory, an intrinsic function, also called built-in function or builtin function, is a function (subroutine) available for use in a given programming language whose implementation is handled specially by the compiler.

# Memory Alignment
To use SIMD, the memory must be aligned.
```
#include <immintrin.h>

#include <iostream>

int main() {
    using aligned_double4 = __attribute__((aligned(32))) double[4];

    double *input1 = (double *)std::aligned_alloc(4 * sizeof(double), 4 * sizeof(double));
    aligned_double4 input2 = {1, 2, 3, 4};
    aligned_double4 result;

    std::cout << "address of input1: " << input1 << std::endl;
    std::cout << "address of input2: " << input2 << std::endl;

    __m256d a = _mm256_load_pd(input1);
    __m256d b = _mm256_load_pd(input2);
    __m256d c = _mm256_add_pd(a, b);

    _mm256_store_pd(result, c);

    std::cout << result[0] << " " << result[1] << " " << result[2] << " " << result[3] << std::endl;
    std::free(input1);

    return 0;
}
```

# Compare to Standard Function
Lower precision but higher performance.

# References
[https://www.intel.com/content/www/us/en/docs/cpp-compiler/developer-guide-reference/2021-8/intrinsics.html](https://www.intel.com/content/www/us/en/docs/cpp-compiler/developer-guide-reference/2021-8/intrinsics.html)