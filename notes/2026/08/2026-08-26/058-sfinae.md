# 模板特化与 SFINAE：调试与观测手法

**日期**：2026-08-26　**领域**：C/C++　**编号**：58/5000

## 背景

先拿到证据再改代码，日志与指标是第一手材料。这里围绕「模板特化与 SFINAE」做一次整理，重点放在能直接落地的部分。

## 要点

- if constexpr 可替代大量 tag dispatch
- concept 让错误信息更友好
- 把排查过程留成记录，下次能少走弯路。

## 示例

```cpp
template <class T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T> T twice(T v) { return v + v; }
```

## 易错点

- 特化必须在同一命名空间且在使用前声明

## 小结

模板特化与 SFINAE 在调试与观测手法这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
