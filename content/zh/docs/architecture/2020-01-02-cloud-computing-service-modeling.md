---
title: "Cloud Computing Service Modeling"
date: 2020-01-02T18:24:11+08:00
draft: false
tags: 
categories: 
- Tech

featured_image: 
description: 
---

## 简介
2020年需要重新思考架构模型，我们以怎样的方式对外提供服务，是Service， 一起看下有哪些Service吧  

## Service Model
常见的应该有Iaas(Host)、Paas(Build)、Saas(Consume)、Faas, 而在这边文章"Future of Cloud Computing Architectrue"里提到的Service更多类型

![Cloud Computing Stack](https://hyvi.github.io/blog-images/20200102/Future%20of%20Cloud%20Computing%20Stack.png)

每一种提供了不同的灵活性和控制，如下图：

![Saas vs Paas vs Iaas Service Model](https://hyvi.github.io/blog-images/20211002/5-layer-diagram.png)

### Function-as-a-service TODO

### Software-as-a-Service
The Saas model 为你的业务提供基于云的web应用的访问能力，无须install new infrastructure   

#### The Twelve-Factor APP
https://12factor.net/  为提供Saas服务提供了方法论:

 - 使用标准化流程自动配置
 - 和操作系统之间尽可能的划清界限，在各个系统中提供**最大的可移植性**
 - 适合**部署**在现代的**云计算平台**， 从而在服务器和系统管理方面节省资源
 - 将开发环境和生产环境的差异降至最低，并使用持续交付实施敏捷开发。
 - 可以在工具、架构和开发流程不发生明显变化的前提下实现扩展。


#### 身份认真和授权 TODO
License Model for Saas or alias "Sass License", 感觉类似“[AWS cognito](https://aws.amazon.com/cn/cognito/dev-resources/)”   
vs IAM   

[文章展示了AWS各个服务之间的交互逻辑](https://aws.amazon.com/cn/blogs/china/aws-kms-enables-secure-data-encryption-across-tenants/)

### Platform-as-a-service
With this model, a third-party vendor provides your business with a platform upon which your business can develop and run application.

### Infrastructure-as-a-service 
allow your business to have complete, scalable control over the management and customization of your infrastructure . 

## Patterns in microservice 
![architecture trends 2020](https://res.infoq.com/articles/architecture-trends-2020/en/resources/1Architecture-2020-Q2-1587042627643.jpg) 

### EDA 
![Service composition - anit pattern](https://miro.medium.com/max/468/1*YPhljs4qcqtN08dA54fdwA.png)

- tightly coupled, because the calling service needs to know the URL payload and related detail of the service it calls 
- a change in functionality require a coordinated effort between multiple teams 


![Event notifications and event-driven architectures](https://miro.medium.com/max/1166/1*TtaEDXMTFpPqHj0a-7lxiw.png) 

### AsyncAPI #TODO

### Data Architecture 

#### Data Mesh 
> the next enterprise data platform architecture is in the convergence of Distributed Domain Driven Architecture, Self-serve Platform Design, and Product Thinking with Data<sup>[5]</sup>.
>    --- Zhamak Dehghani

#### Data Gateways 
somewhat like API gateways but focus on the data aspect.

### Policy as Code #TODO

### Designing for ___

#### Designing for resilience

#### Designing for abservability

#### Designing for portability
whether that’s for multi-cloud or hybrid-cloud. In most cases, there are no reasons for architects to design for the lowest common denominator to enable true multi-cloud portability or avoiding vendor lock-in. 

#### Designing for sustainability
This is emerging because people are realizing the software industry is responsible for a level of carbon usage comparable to the aviation industry<sup>[6]</sup>.

### Dapr 

{{< youtube id="eJCu6a-x9uo" title="Nark Russinovich: The Future of Cloud Natvie Applications with Open Application Model and Dapr" >}}

It is describing as a set of"microservice building blocks for cloud and edge" also is meant to be agnostic

> Dapr is completely platform agnostic, meaning you can run your applications locally, on any Kubernetes cluster, and other hosting environments that Dapr integrates with. This enables developers to build microservice applications that can run on both the cloud and edge with no code changes,"

![Dapr is a portable, event-driven, runtime for building distributed applications across cloud and edge.](https://github.com/dapr/dapr/raw/master/img/overview.png)

#### Dapr building blocks

- Service Invocation 
- State management 
- Plubish and subscribe messaging between services 
- Event driven resource bindings 
- Virtual actors --  A pattern for stateless and stateful objects that make concurrency simple with method and state encapsulation. Dapr provides many capabilities in its virtual actor runtime including concurrency, state, life-cycle management for actor activation/deactivation and timers and reminders to wake up actors<sup>[7]</sup>.
- Distributed tracing between services 
- Resillency 

#### Sidecar architecture and supported infrastructures
Dapr exposes its APIs as a sidecar architecture, either as a container or as a process, not requiring the application code to include any Dapr runtime code.

![Dapr running as a side-car process](https://cloudblogs.microsoft.com/uploads/prod/2019/10/overview-sidecar.png)

#### Multi-Cloud, open components (bindings, pub-sub, state) from Azure, AWS, GCP
Dapr is completely platform agnostic, meaning you can run your applications locally, on any Kubernetes cluster, and other hosting environments that Dapr integrates with. This enables developers to build microservice applications that can run on both the cloud and edge with no code changes.
#### Dapr 和 Service-Mesh 的区别
![service-mesh vs dapr](https://docs.dapr.io/images/service-mesh.png)

共同点： 

- 基于 mTLS 加密的服务到服务的安全通信
- 服务到服务的度量指标收集
- 服务度到服务的分布式跟踪
- 故障重试恢复能力

Dapr 以开发者为中心，提供了通过了名称进行服务发现和调用的方式。Dapr 还提供了其他应用级的构建块，如状态管理、发布/订阅、参与者等


## Principles in Microservice

1. Create an organizational model that provide independence and antonomy to teams 
2. services are independently deployable
3. services are independently scalable 
4. they do not have a single point of failure - only degradation 
5. the design employ asynchronous communication between services 
6. no shared functionality , code or data exists in the system .
7. Component are easy to understand and the are small services with boundary 

## 思考
接触到“AWS解决方案架构师”，负责企业客户应用在AWS的架构咨询和设计。在微服务架构设计，数据库等领域有丰富的经验。  
是技术产品还是技术架构师呢？ 那AWS这些云产品由什么位置来规划的？  
是技术架构师又偏技术业务，这是云服务架构师的之路, 最后做技术架构咨询。 


## TODO 

[ ] 企业软件架构模式，见kami app

## 参考

[1] [Futrue of Cloud Computing Architecture.pdf](https://www.sjsu.edu/people/robert.chun/courses/CS247/s4/I.pdf)  

[2] IBM: IaaS vs. PaaS vs. SaaS, Understand and compare the three most popular cloud computing service models

[3] InfoQ: Software Architecture and Design InfoQ Trends Report—April 2020

[4] InfoQ 趋势报告：架构和设计领域技术演变详解 2019

[5] Zhamak Dehghani: How to Move Beyond a Monolithic Data Lake to a Distributed Data Mesh 

[6] Thomas Betts, Holly Cummins: Software Architecture and Design InfoQ Trends Report -- April 2021

[7] Microsoft Open Source Blog: Announcing Distributed Application Runtime (Dapr), an open source project to make it easier for every developer to build microservice applications

<br>

<center>  ·End·  </center>
