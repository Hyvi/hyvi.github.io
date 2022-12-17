---
title: "API 兼容性设计"
date: 2019-09-25T22:56:31+08:00
draft: false
tags: 
  - API 
categories: 
  - Tech 
featured_image: 
description: 
---

## 简介
向后兼容的一般目标是： 服务升级到新的minor版本或者patch后客户端不应该被破坏  

## 名词解释
### Source Compatibility 
code that compiled against version X of an API will also compile against version Y . 
### Binary Compatibility 
code that compiled against version X of an API will run correctly in an environment that has version Y of the same API. 

## 向后兼容性的改变

- 为API服务添加一个API接口
- 为API接口添加一个方法
- 为方法添加一个HTTP绑定
- 为请求消息添加一个字段
- 为响应消息添加一个字段 
- 为枚举类型添加一个值 
- 添加output-only的资源字段  


## 不向后兼容的更改

- 删除或重命名一个服务，字段或者枚举值
- 更改HTTP绑定
- 更改某个字段类型
- 更改资源名称格式 
- 修改已有请求的可见性 
- 在HTTP定义中改变URL格式
- 在资源消息中添加读/写字段   

## 参考 
[ Google API 设计指南 - 兼容性 ](https://segmentfault.com/a/1190000009157548#articleHeader14)   
[ Backward Compatibility Guidelines ](https://developers.google.com/youtube/compatibility_guidelines)  
[ API Gesign Guide ](https://google-cloud.gitbook.io/api-design-guide/) Google针对网络API的通用设计指南  
[ API Compatibility v2](https://github.com/kijiproject/wiki/wiki/API-Compatibility-v2) 
[ Stripe With versioning ][1], 解决版本、文档、变更问题。

[1]: https://stripe.com/blog/api-versioning

<br>

<center>  ·End·  </center>
