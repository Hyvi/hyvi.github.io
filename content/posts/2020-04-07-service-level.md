---
title: "Service Level Ojbect vs Service Level Agreement"
date: 2020-04-07T14:28:02+08:00
draft: false
tags:
categories:
featured_image:
description:
---
诸多的微服务，微服务的状态是怎样的，目前是心里没底的，通过 SLA 指标来衡量服务的状态。

# 可选的指标

## Availability Rate
可用性，常见的多少个 9.

## Request Rate

## Error Rate

## Latency
response time， including queue/wait time, in millisecornds

## Saturation
how overloaded something is, directly measured by things like queue depth (or something concurrency) ,  saturation is usually more useful for alerts

## Utilization
how busy the resource or system is , Usually expressed 0-100% and most useful for prediction

# 参考
1. SLA vs SLO 其中有一些可以参考的例子，比如 "25 Examples of a Service Level Objective
  https://simplicable.com/new/sla-vs-slo

2. Monitoring SRE golden signals 文档介绍了 Load balancers's golden signals, web servers' golden signals, App servers' golden signals, Databases' golden signals, Operating systems's golden signals
  https://www.infoq.com/articles/monitoring-SRE-golden-signals/


<br>

<center>  ·End·  </center>
