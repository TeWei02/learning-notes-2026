# multiprocessing 与 GIL 的取舍：代码评审关注点

**日期**：2026-08-28　**领域**：Python　**编号**：42/9000

## 背景

评审优先看契约与失败路径，其次才是实现技巧。这里围绕「multiprocessing 与 GIL 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- CPU 密集用多进程，IO 密集用线程或 asyncio
- 多进程传参需可 pickle，大对象建议用共享内存
- 把重复出现的意见沉淀成团队约定。

## 示例

```python
with ProcessPoolExecutor(max_workers=8) as ex:
    results = list(ex.map(heavy, chunks))
```

## 易错点

- 子进程里的全局状态不会回传，注意初始化逻辑

## 小结

multiprocessing 与 GIL 的取舍 在代码评审关注点这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
