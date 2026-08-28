# CORS 预检请求触发条件：常见陷阱与错误示范

**日期**：2026-08-28　**领域**：Web　**编号**：79/9000

## 背景

多数线上问题不是不会用，而是用错了一个细节。这里围绕「CORS 预检请求触发条件」做一次整理，重点放在能直接落地的部分。

## 要点

- 非简单方法或自定义头部会触发 OPTIONS 预检
- 带凭据时 Access-Control-Allow-Origin 不能为通配
- 把踩过的坑写成检查项，比背结论更有效。

## 示例

```js
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

## 易错点

- 预检结果可缓存，但需要服务端给 Max-Age

## 小结

CORS 预检请求触发条件 在常见陷阱与错误示范这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
