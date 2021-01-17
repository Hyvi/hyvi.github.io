---
title: "Microservice Arch 点点滴滴"
date: 2020-05-08T17:25:13+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

## 对标行业架构最佳实践

[Best practices framework for Oracle Cloud Infrastructure](https://docs.oracle.com/en/solutions/oci-best-practices/index.html#GUID-5F2D2745-934E-409A-A7BA-D0976F727845) *TODO*



## 主题

###  request_id 

[Better Logging Approach For Microservices](https://medium.com/cstech/better-logging-approach-for-microservices-3cc2c45e7aaa) request_id在日志中打印，由请求方生成发起

从[What is the X-REQUEST-ID http header?](#参考)说明来看，建议是client生成x-request-id.


### RateLimiter 

限流的基础算法

- 漏桶算法
  - 漏桶算法的实现往往依赖于队列，请求到达如果队列未满则直接放入队列，然后有一个处理器按照固定频率从队列头取出请求进行处理。 如果请求量大，则会导致队列满，那么新来的请求就会被抛弃。

![](https://upload-images.jianshu.io/upload_images/623378-d8ca6373e1fbddae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 令牌桶算法
  - 一个存放固定容量令牌的桶，按照固定速率往桶里添加令牌。桶中存放的令牌数有最大上限，超出之后 就会被丢弃或拒绝。当流量或者网络请求到达时，每个请求都要获取一个令牌，如果能获取到，则直接处理，并且令牌桶删除一个令牌。如果获取不到，则该请求就要被限流，要么直接丢弃，要不再缓冲区等待。

  - 长期来看，所限制的请求速率的平均值等于 rate（每秒向桶添加令牌的速率r） 的值
  - 实际请求达到的速率为 M， 达到的最大速率为 M = b + r (其中b 为令牌桶的最大值)

![](https://upload-images.jianshu.io/upload_images/623378-992f9c0b0ab82143.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


<br>

## 参考

1. What is the X-REQUEST-ID http header?
  https://stackoverflow.com/questions/25433258/what-is-the-x-request-id-http-header) 

<center>  ·End·  </center>
