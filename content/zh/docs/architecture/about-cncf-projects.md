---
title: "About Cncf Projects"
date: 2020-05-10T18:11:23+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
CNCF Project vs CNCF Member Project 这有什么区别？ 

## Projects
### OpenTelemetry
OpenTelemetry 在遇到以下无法解决的问题情况下出现了。

- 应用程序被锁定在特定解决方案的仪表中
- 针对开源软件的特定解决方案的仪表基本上是不可能的

于是需要设计一个可观测的系统来解决以上问题，在设计上需要满足基本的需求<sup>[4]</sup>：

- 要求：独立的仪表(instrumentation，这个翻译总觉得怪异，)、遥测和分析
- 要求：零依赖性
- 要求：严格的后向兼容和长期支持


#### 概念


##### 信号 signal
不同类型的遥测，我们称之为**信号**，主要的信号是追踪

OpenTelemetry 是一个跨领域的关注点(cross-cutting concern)

![](https://raw.githubusercontent.com/rootsongjc/cloud-native-library/master/content/opentelemetry-obervability/images/f5-1.png "所有 OpenTelemetry 信号都建立在一个共享的上下文传播系统之上。其他的，非可观测性的交叉关注也可以使用上下文传播机制来通过分布式系统传输他们的数据。")


##### Instrumentation
仪表（在 《OpenTelemetry 可观测性的未来》这样翻译的）

但是，来自谷歌：the particular instruments used in a piece of music / measuring instruments regarded collectively.

##### OTLP 

OpenTelemetry protocol (OTLP)， 定义了 Open Telemetry 里 Tracing\Metrics\Logging 的 protobuf 的协议格式。 比如 [ Tracing ](https://github.com/open-telemetry/opentelemetry-proto/blob/main/opentelemetry/proto/trace/v1/trace.proto) 


##### Propagators and Context

Propagators: Used to serialize and deserialize specific parts of telemetry data such as span context and Baggage in Spans.

Traces can extend beyond a single process. This requires context propagation, a mechanism where identifiers for a trace are sent to remote processes.


```golang
otel.SetTextMapPropagator(propagation.TraceContext{})
```

`TextMapPropagator` injects values into and extracts values from carries as text.

##### Carrier
A carrier is the medium used by Propagators to read values from and write values to.

#### 结合 Newrelic Tracing 的实践
[ OpenTelemetry and Newrelic 结合 ](https://docs.newrelic.com/docs/integrations/open-source-telemetry-integrations/opentelemetry/opentelemetry-quick-start/), 中间通过 opentelemetry-go 来连接。 

![](https://docs.newrelic.com/44724d5e137a64a9b9f426e1bcddc445/native_otlp.svg)

也可以通过 opentelemetry-collector (e.g. binary, sidecar, or daemonset). 方式来做。

![](https://docs.newrelic.com/2500a84a188882f4b0ecf1d270689112/native_otlp_with_collector.svg) 

#### 结合 Alibaba Tracing Analysis（ARMS）的实践
[What is Tracing Analysis](https://www.alibabacloud.com/help/en/application-real-time-monitoring-service/latest/what-is-tracing-analysis)， 从 Architecture 看是支持 Opentracing Basing SDK

> Tracing Analysis is compatible with SDKs from various open source communities and supports the OpenTracing standard.


### Apache DolphinScheduler
A distributed and easy-to-extend visual workflow scheduler system, undergoing incubation at ASF.


### MegaEase 
开源、自主可控、低层本、高可用的 Cloud Native 平台

- 服务编排和服务治理
- 流量调度和流量管理
- 应用服务观测性 & DevOps
- 关键中间件运维及管理
- 基础资源调度

![](https://megaease.com/imgs/cloud.native.stack.zh.png) 

![](https://megaease.com/imgs/cloud.native.arch.zh.png) 




## 参考

1. [OpenTelemetry-可观察性的新时代 ](https://juejin.im/post/5d3572c1e51d45776147620f)

2. [CNCF 项目或者成员项目](https://landscape.cncf.io/project=member)

3. OpenTelemetry: Propagators API

4. Ted Young，译者 Jimmy Song: OpenTelemetry可观察性指南

<br>

<center>  ·End·  </center>
