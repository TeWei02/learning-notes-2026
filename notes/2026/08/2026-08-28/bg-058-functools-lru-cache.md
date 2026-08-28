# functools.lru_cache 的缓存键：实现原理与内部机制

**日期**：2026-08-28　**领域**：Python　**编号**：58/9000

## 背景

知道底层怎么走，行为异常时才能判断卡在哪一层。这里围绕「functools.lru_cache 的缓存键」做一次整理，重点放在能直接落地的部分。

## 要点

- 参数必须可哈希，传 list 会直接 TypeError
- cache_info 的 hits/misses 是定位热点的第一手数据
- 原理清楚后，参数上限与限制条件基本能自己推导。

## 示例

```python
@lru_cache(maxsize=512)
def fetch(code: str, market: str) -> float:
    return _query(code, market)
```

## 易错点

- 带默认值的可选参数会造成多份缓存，建议显式传参

## 小结

functools.lru_cache 的缓存键 在实现原理与内部机制这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
