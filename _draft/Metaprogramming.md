---
layout:     post
title:      "Metaprogramming"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - C++
---

# Example
## Type traits
Check whether T is a specified type:
```
template <typename T>
struct is_vector_type : std::false_type {};
template <typename U>
struct is_vector_type<std::vector<U>> : std::true_type {};
template <typename T>
inline constexpr auto is_vector_type_v = is_vector_type<T>::value;
```

Check whether a struct has a field:
```
#include <type_traits>

template <typename T, typename = int>
struct HasX : std::false_type { };

template <typename T>
struct HasX <T, decltype((void) T::x, 0)> : std::true_type { };
```

Variadic templates:
```
template <typename Fn, typename std::size_t... I>
inline constexpr void ExecAtComplie(Fn fn, std::index_sequence<I...>) {
    using Expander = int[];
    (void)Expander{0, ((void)fn(I), 0)...};
}
```