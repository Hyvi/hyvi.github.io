---
title: "What We Concern"
date: 2020-01-07T20:03:54+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
plantuml: true
---

# 背景

# 我们的问题

## 效率
效率，不只是开发、测试、需求，指的是迭代上线的效率。

## 业务的价值和清晰
做有价值的业务, 并有清晰的规划   

- 缺乏严格的需求评审

# 我们的改变

## 提高效率

- 更改目前发版的流程， 不需要建版本，在发版完即可通知相关方。
- 更改目前的测试方式， 推动接口测试+单元测试， 不依赖与APP测试。
- 着力中台, 沉淀公共业务领域，提高小前台的的迭代速度
- 引入devops, 释放developer的参与的运维工作 

## 清晰的业务和价值 

- 需求流程优化
- 加强需求评审

## 应用能力平台化
### [行业对标] 金融生态云
内容来自： [银行生态云建设思路及架构参考][back-cloud-architecture]

#### 技术路线
```plantuml
@startuml

actor "开发人员" as dev 
actor "产品&运营人员" as run 


skinparam RectangleFontName Papyrus
skinparam RectangleFontSize 24
rectangle " 云服务开发规范 " as spec {

}

rectangle "基础云平台"  as plat {
    rectangle "基础服务平台" as basic
    rectangle "安全接口" as basic1
    rectangle "审计接口" as basic2
    rectangle "计量接口" as basic3
    rectangle "计费接口" as basic4

    basic -> basic1 
    basic -> basic2
    basic -> basic3
    basic -> basic4
    basic1 -[hidden]-> basic2
    basic2 -[hidden]-> basic3
    basic3 -[hidden]-> basic4
}


rectangle "标准云产品" as product {

    rectangle "安全接入" as a 
    rectangle "计量接入" as b
    rectangle "审计接入" as c

    a -[hidden]-> b 
    b -[hidden]-> c
}
'spec -[hidden]-> plat
plat --> spec: 云平台提供标准的开发规范和接口

product -> plat: 通过接口接入，在运营平台上自动接入

spec --> dev: 指导开发

dev -> product: 开发人员遵循开发规范


run --> product
@enduml
@enduml
```

"开放云平台+标准产品”的方式成就了**典型生态云的持续运营能力**。开放的云平台提供云基础服务，并以标准接口的方式把这些基本服务暴露给云产品开发人员。


```plantuml
@startmindmap

* 生态云技术路线
** 标准开放的云平台
*** 核心能力
**** 标准开放框架
*****_: 标准的开放框架是生态云能健康持续发展的基础，
定义了云服务构建的技术标准，允许快速开发标准产品
;
**** 产品服务能力？
*****_ 产品服务能力是生态云的价值体现。
**** 安全服务能力
*****_ 为云平台和云服务的租户提供**体系化**的安全管理能力
**** 持续运营能力
*****_: 提供客户运营、云服务产品运营及平台运营能力，
实现标准云产品的生命周期管理，实现客户自主服务。
;
**** 集中管控能力
*****_ 实现云资源和业务应用的统一管理、调度和监控、底层资源的扩缩容管理

** 标准产品
@endmindmap
```
## 物联网平台化 - IoT
这块知识是2020年需要成长的地方，硬件为主，赋能硬件是后续的趋势。 

### [行业对标] Google Cloud IOT
#### 实践
### 阿里云 IOT
#### 实践

### [行业对标] EMQ X

1. 关键技术
    - 分布式
    - 容器化
    - 桥接
2. 核心指标
    - 多协议
    - 并发量： 单服务器200万并发, 一个集群1000万并发(7个节点）
    - 吞吐量： 单集成百万并发

#### 实践

## 解决方案 
明星产品, 比如xxx

新产品设备?
# 参考
1. MQTT ESSENTIALS by HIVEMQ团队整理 https://www.hivemq.com/mqtt-essentials/ 
    - MQTT Basic
    - MQTT Features
    - MQTT Specials
2. 初识MQTT https://developer.ibm.com/zh/articles/iot-mqtt-why-good-for-iot/ 
    - 为什么是MQTT而不是其他协议
    - MQTT协议是怎样的

3. EMQ X https://github.com/emqx/emqx

4. NATS 
    - Does NATS support MQTT? https://github.com/nats-io/nats-server/issues/812
        - 分支开发中，预计在Q4支持
    - 支持持久化存储 File Store / SQL Store [Persistence][nats-persistence]
  

[nats-persistence]: https://docs.nats.io/nats-streaming-server/configuring/persistence
<br>

[back-cloud-architecture]: https://cloud.tencent.com/developer/article/1485632
<center>  ·End·  </center>
