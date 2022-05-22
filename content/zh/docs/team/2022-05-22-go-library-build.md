---
layout: post
title: "如何构建基础库"
date: 2022-05-22
draft: false
description: 
featured_image: 
tags: 
 - 架构
categories: 
 - Tech
---

## 简介
提供一个库，沉淀共性的功能点。

是Library，而不是 Framework。

有哪些内容呢？



## 参考1 Gitlab Labkit
LabKit is minimalist library to provide functionality for Go services at GitLab.

- Correlation
- **Loggging**
- Masking
- **Metrics**
- **Monitoring**
- FIPS
- **Tracing**
- **ErrorTracking**

## 参考2 go-zero

- 鉴权
- 加解密
- 日志记录
- 异常捕获
- 监控报警
- 数据统计
- 并发控制
- 链路追踪
- 超时控制
- 自动熔断
- 自动降载
- 缓存控制

![](https://raw.githubusercontent.com/zeromicro/zero-doc/main/doc/images/architecture.png)

## 参考3 go-micro

[Micro Architecture](https://micro.dev/architecture)

![](https://micro.dev/images/micro-3.0.png)


## 参考4 Dapr
