# logging 的传播与层级：版本迁移与兼容处理

**日期**：2026-08-28　**领域**：Python　**编号**：115/9000

## 背景

升级前先确认依赖链上的行为差异。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 灰度期间保留回退路径。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在版本迁移与兼容处理这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
