# Kubernetes 探针设计：代价与适用边界

**日期**：2026-08-28　**领域**：工具　**编号**：33/9000

## 背景

任何方案都有不适用的时候，提前写清楚。这里围绕「Kubernetes 探针设计」做一次整理，重点放在能直接落地的部分。

## 要点

- 存活探针用于重启恢复，就绪探针用于摘流量，语义不能混用
- 启动慢的服务用 startupProbe 避免被误杀
- 把不适用条件写进文档，避免误用。

## 示例

```yaml
startupProbe: { periodSeconds: 5, failureThreshold: 30 }
livenessProbe: { httpGet: { path: /healthz, port: 8080 } }
```

## 易错点

- 就绪探针依赖外部下游会导致整体抖动

## 小结

Kubernetes 探针设计 在代价与适用边界这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
