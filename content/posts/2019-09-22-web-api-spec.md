---
title: "Web Api Spec"
date: 2019-09-22T00:22:23+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

# 背景
后台服务对外最重要的是提供API接口，上百上千的接口，怎么保持一种规范/约束，才能让接口在创建、更新、废弃生命周期中是有据可循的呢？ 

* 接口的创建是按照什么规范?  
* 接口的更新是对业务方无影响或者影响非常小的？  
* 接口的废弃是怎样的方式？  

# 调研
## 业界解决方案 

### apiary  

- Support API Blueprint\Swagger API  

> DNA for your API --- powerful, open sourced and developer-friendly. The ease of Markdown combined with the power of automated mock server , tests, validations, proxies, and code samples in your language bindings    

- Server Mock
- Documentation
- Traffic Inpspector  

### [MuleSoft](https://www.mulesoft.com/platform/api/manager) 
the most widely used integration platform  

总结： 有接口管理、实时使用数据指标、流量突变告警、

###  [APIMATIC](https://www.apimatic.io/)
- instant SDK, Code Samples, Test Cases  
- Continuous Code Generation
- API Transformer

总结： 其中代码生成、持续的代码生成、API转换都是非常需要的功能。  

###  [Apigee ](cloud.google.com/apigee)  
google提供跨云环境的API管理

* Web API Design 
* Mastering Full Lifecycle API 
* Management with Analytics 
* Securing APIs in the Age of Connected Experiences 

总结： 基本上满足文章开头的三个问题。  

### Kong 
介绍很少  
### 其他

* [apigility ]( www.apigility.org )  
* [Falcon]() Python web framework   
* [Amazon API Gateway]() traffic management, authorization and access control, monitoring and API version management  
## 公司解决方案

# 结论 
## 一期
API生命周期管理：API新建和显示（For Humans, For Machines）， API使用， API弃用, 版本管理， 授权与访问控制   

### TODO LIST

## 二期
API的健康状态管理： API流量、API错误率等。打通与APM之间的数据。
### TODO LIST
## 三期
支持更多的功能： API在线编写， API不规范的提示，API调式，API MOCK，API自动测试，代码生成（SDK和sample），

- Traffic Inspector   
提供代理方式，开发者可以把数据发送到调试代理上，通过比对数据和协议内容，来定位问题。[想法来自 apiary.io](apiary.io)  

### TODO LIST
# 参考 

[The Web API Checklist -- 43 Things To Think About When Designing, Testing, and Releasing your API](https://mathieu.fenniak.net/the-api-checklist/)  
[理解HTTP幂等性](https://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html)   
[API EVANGELIST](http://design.apievangelist.com)  
[API Blueprint](https://apiblueprint.org)  
[13 Free & Open Source Tools For API Creation, Management & Testing](https://www.how2shout.com/tools/free-open-source-tools-api-creation-management-testing.html#comments)  


<br>

<center>  ·End·  </center>
