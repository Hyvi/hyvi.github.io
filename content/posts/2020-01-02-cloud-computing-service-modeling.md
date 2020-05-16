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

# 简介
2020年需要重新思考架构模型，我们以怎样的方式对外提供服务，是Service， 一起看下有哪些Service吧  

# Service Model
常见的应该有Iaas(Host)、Paas(Build)、Saas(Consume)、Faas, 而在这边文章"Future of Cloud Computing Architectrue"里提到的Service更多类型
![Cloud Computing Stack](https://hyvi.github.io/blog-images/20200102/Future of Cloud Computing Stack.png)
每一种提供了不同的灵活性和控制，
![Saas vs Paas vs Iaas Service Model](https://www.paranet.com/hs-fs/hub/107491/file-16287446-png/images/cloud_computing_service_models.png?width=1520&name=cloud_computing_service_models.png) 

## Function-as-a-service TODO

## Software-as-a-Service
The Saas model 为你的业务提供基于云的web应用的访问能力，无须install new infrastructure   

### 身份认真和授权 TODO
License Model for Saas or alias "Sass License", 感觉类似“[AWS cognito](https://aws.amazon.com/cn/cognito/dev-resources/)”   
vs IAM   

[文章展示了AWS各个服务之间的交互逻辑](https://aws.amazon.com/cn/blogs/china/aws-kms-enables-secure-data-encryption-across-tenants/)

## Platform-as-a-service
With this model, a third-party vendor provides your business with a platform upon which your business can develop and run application.

## Infrastructure-as-a-service 
allow your business to have complete, scalable control over the management and customization of your infrastructure . 

# Patterns in microservice 
![architecture trends 2020](https://res.infoq.com/articles/architecture-trends-2020/en/resources/1Architecture-2020-Q2-1587042627643.jpg) 

## EDA 
![Service composition - anit pattern](https://miro.medium.com/max/468/1*YPhljs4qcqtN08dA54fdwA.png)

- tightly coupled, because the calling service needs to know the URL payload and related detail of the service it calls 
- a change in functionality require a coordinated effort between multiple teams 


![Event notifications and event-driven architectures](https://miro.medium.com/max/1166/1*TtaEDXMTFpPqHj0a-7lxiw.png) 

## AsyncAPI #TODO

## Data Mesh #TODO

## Policy as Code #TODO

# Principles in Microservice

1. Create an organizational model that provide independence and antonomy to teams 
2. services are independently deployable
3. services are independently scalable 
4. they do not have a single point of failure - only degradation 
5. the design employ asynchronous communication between services 
6. no shared functionality , code or data exists in the system .
7. Component are easy to understand and the are small services with boundary 

# 思考
接触到“AWS解决方案架构师”，负责企业客户应用在AWS的架构咨询和设计。在微服务架构设计，数据库等领域有丰富的经验。  
是技术产品还是技术架构师呢？ 那AWS这些云产品由什么位置来规划的？  
是技术架构师又偏技术业务，这是云服务架构师的之路, 最后做技术架构咨询。 

# 参考

[Futrue of Cloud Computing Architecture.pdf](https://www.sjsu.edu/people/robert.chun/courses/CS247/s4/I.pdf)  
[Which Cloud Computing Service Model is Right for Your Business](https://www.paranet.com/blog/bid/128267/the-three-types-of-cloud-computing-service-models)  

3. Software Architecture and Design InfoQ Trends Report—April 2020
  https://www.infoq.com/articles/architecture-trends-2020/

4. InfoQ 趋势报告：架构和设计领域技术演变详解 2019
  https://www.infoq.cn/article/R7lWXd0R4VFf3E0bB*38
<br>

<center>  ·End·  </center>
