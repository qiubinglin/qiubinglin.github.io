---
layout:     post
title:      "C++ Concept"
subtitle:   "初见C++20"
date:       2022-11-25 11:03:00
author:     "Bing"
catalog:    true
tags:
    - 编程
    - C++
    - C++20概念
---

# Concept是什么
Concept是编译器谓词。在泛型编程或模板元编程中使用能够大大增强语义性、规范模板的使用并减少错误地使用模板时编译器混乱的错误信息。

# Concept的定义
定义Concept和定义普通的模板方式很类似，需要注意的是新引入的关键字 $requires$ 的用法。

**可哈希谓词**
```
template <typename T>
concept Hashable = requires(T a) {
    { std::hash<T>{}(a) } -> std::convertible_to<std::size_t>; // 即是要求对a做哈希的结果可以转换成std::size_t类型
};
```

**相等性可比较谓词**
```
template <typename T, typename U = T>
concept Equality_comparable = requires(T a, U b) {
    // 两条约束
    { a == b } -> bool ;
    { a != b } -> bool ;
};
```

**方法存在性谓词**
```
template <typename T>
concept HasFuncA = requires(T t) {
    t.FuncA();
}
```
```
template <typename T>
concept HasFuncB = requires(T t, int num) {
    t.FuncB(num);
}
```

# Concept的使用
**在模板中使用**
```
template <Hashable T>
void f(T a) {
    // ...
}

template <typename T, typename U>
    requires Equality_comparable<T, U>
void f(T a, U b) {
    // ...
}
```

**结合auto使用**
```
Hashable auto f(Hashable auto a) {
    // return some type hashable
}
```

**偏特化**
```
template <typename T>
struct HashMap {
    std::string toHash() const requires Hashable<T> {
        ...
    }
};
```

```
template <typename T>
struct Writer {
    void WriteAsHash(const std::string &path) requires(Hashable<T> == true) {
        // hash and write
    }

    void WriteAsHash(const std::string &path) requires(Hashable<T> == false) {
        // do nothing
    }
};
```