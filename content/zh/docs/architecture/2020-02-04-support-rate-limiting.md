---
title: "限流的那些事"
date: 2020-02-04T16:03:54+08:00
draft: false
tags:
categories:
featured_image:
description:
---

## 背景
限制 API 的请求数量是网络安全的一部分，大量的 API 请求导致高负载。
在学习 rudr 过程中也提到 rate limiting 可以做为 trait， 那么使用起来非常方便，业务开发并不需要关心限流逻辑。

## Glossary

**traffic shaping**

packet are delayed until they conform

**traffic policing**

non-conforming packets may be discarded(dropped) or may be reduced in priority.
## What and The Importance


### What Is API Rate Limiting

集群流控： 集群流量不均匀导致总体限流效果不佳的问题，仅靠单机纬度去限制的话无法精准限制总体流量。
### Best Practices For API Rate Limiting

### How to Throttle API Calls

### Three Methods of Implementing API Rate-Limiting

#### Adaptive System Protection （系统自适应限流）

- Load 自适应
- CPU usage
- 平均 RT
- 并发线程数
- 入口 QPS

#### Request Queues


#### Throttling
API Used by setting up a temporary state, allowing the API to assess each request

#### Rate-limiting Algorithms

**Leaky Bucket**

- as a meter，与 Token bucket 算法互为 mirror，
	- Token bucket 固定的 rate 增加 token；而另外一个是 固定的 rate 漏水
	- Token bucket 请求从桶中获取 token, 获取不到时则限流；而另外一个是往漏斗中滴水，滴满时则限流。
- as a queue，用于匀速排队的方式严格控制请求通过的间隔时间。

**Fixed Window**

**Sliding Log**

**Sliding Window**



## Rate Limiting 影响




## 参考
1. Everything You need to Know About API Rate Limiting
  https://nordicapis.com/everything-you-need-to-know-about-api-rate-limiting/

2. Sentinel: 集群流控，https://github.com/alibaba/Sentinel/wiki/集群流控
<br>

<center>  ·End·  </center>
