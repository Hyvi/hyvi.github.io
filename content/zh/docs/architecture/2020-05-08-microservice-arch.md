---
title: "Microservice Arch 点点滴滴"
date: 2020-05-08T17:25:13+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

![image via: https://www.infoq.com/presentations/uber-microservices-distributed-tracing/](https://www.jrebel.com/sites/rebel/files/image/2020-04/sl9-1567597621813-min.jpg)

## Pattern: microservice architecture

"An architectural style that structures an application as a set of deployable/executable units, a.k.a. services"

- Highly maintainable and testable
- Minimal lead time (time from commit to deploy)
- Loosely coupled
- Independently deployable
- Implements a business capability
- Owned/developed/tested/deployed by a small team

## 行业架构最佳实践

[Best practices framework for Oracle Cloud Infrastructure](https://docs.oracle.com/en/solutions/oci-best-practices/index.html#GUID-5F2D2745-934E-409A-A7BA-D0976F727845) *TODO*

## 行业架构分享
不断更新行业的一些架构分享，进行分析总结。

###  Designing loosely coupled services[Slides]
by Chris Richardson, 介绍了几种类型 coupling 及其缺点和如何设计 loosely coupled 微服务.

Runtime coupling，订单服务需要等待客户服务返回时才给出响应，减少了可用性

Design time coupling，当客户服务变化时，订单服务也跟着变化。减少了开发的独立性


Minimizing design time coupling

- DRY 
- Consume as little as possible
- Icebergs: expose as little as possible
- Using a database-per-service

Reducing runtime coupling

- [Use resilience patterns for synchronous communication](#resilience-patterns---circuit-breaker)
- Self-contained service
- Improving availability: replace service with module
- Use asynchronous messaging 
- Improving availability: sagas
- Improving availability: move responsibility + CQRS

Avoiding infrastructure coupling

- Use private infrastructure: minimizes resource contention and blast radius
- Use "Private" message brokers
- Fault isolated swim lanes


##  模式 PATTERNS

### Resilience Patterns - Circuit Breaker 
" used to limit the amount of requests to a service based on configured thresholds -- helping to prevent the service from being overloaded "

同时，通过监控多少个请求失败了，来阻止其他的请求进入到服务里

CircuitBreaker 使用 sliding window 来存储和集合发生的请求。 可以选择 count-based 也可以选择 time-based。

![Image via: https://docs.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker](https://www.jrebel.com/sites/rebel/files/image/2020-04/circuit%20breaker%20illustration.JPG)

### Resilience Patterns - Bulkhead
" Isolates services and consumers via **partitions** ",  舱壁模式, 在航运领域，舱壁是船的一部分，合上舱口后可以保护船的其他部分。

- SemophoreBulkhead, work well across a variety of threading and io models. it is based on a semaphore.
- ThreadPoolBulkhead, uses a bounded queue and a fixed thread pool.

防止级联失败发生. 但对应用来说该模式增加了负担.

![image via: https://www.jrebel.com/blog/microservices-resilience-patterns](https://www.jrebel.com/sites/rebel/files/image/2020-04/image-jrebel-blog-microservices-performance-vector-7.jpg)

什么时候使用：

- Isolate resources used to consume a set of backend services, especially if the application can provide some level of functionality even when one of the services is not responding.
- Isolate critical consumers from standard consumers
- Prodect the application from cascading failures

### Request_id 

[Better Logging Approach For Microservices](https://medium.com/cstech/better-logging-approach-for-microservices-3cc2c45e7aaa) request_id在日志中打印，由请求方生成发起

从[What is the X-REQUEST-ID http header?](#参考)说明来看，建议是client生成x-request-id.


### Resilience Patterns - RateLimiter 

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

What is the X-REQUEST-ID http header? https://stackoverflow.com/questions/25433258/what-is-the-x-request-id-http-header) 

Resilience4j is a fault tolerance library designed for Java8 and functional programming https://github.com/resilience4j/resilience4j


<center>  ·End·  </center>
