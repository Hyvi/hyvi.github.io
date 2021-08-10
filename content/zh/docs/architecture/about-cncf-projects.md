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

#### 概念

**OTLP** 

OpenTelemetry protocol (OTLP)， 定义了 Open Telemetry 里 Tracing\Metrics\Logging 的 protobuf 的协议格式。 比如 [ Tracing ](https://github.com/open-telemetry/opentelemetry-proto/blob/main/opentelemetry/proto/trace/v1/trace.proto) 


#### 实践
[ OpenTelemetry and Newrelic 结合 ](https://docs.newrelic.com/docs/integrations/open-source-telemetry-integrations/opentelemetry/opentelemetry-quick-start/), 中间通过 opentelemetry-go 来连接。 

![](https://docs.newrelic.com/44724d5e137a64a9b9f426e1bcddc445/native_otlp.svg)

也可以通过 opentelemetry-collector (e.g. binary, sidecar, or daemonset). 方式来做。

![](https://docs.newrelic.com/2500a84a188882f4b0ecf1d270689112/native_otlp_with_collector.svg) 

### Apache DolphinScheduler
A distributed and easy-to-extend visual workflow scheduler system, undergoing incubation at ASF.



## 参考
OpenTelemetry-可观察性的新时代 https://juejin.im/post/5d3572c1e51d45776147620f

CNCF 项目或者成员项目 https://landscape.cncf.io/project=member







<br>

<center>  ·End·  </center>
