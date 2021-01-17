---
title: "K8S Request vs Limit"
date: 2020-04-08T17:25:46+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
不断有pod被重启，但是并不知道原因

# 名词解析
`BestEffort`: for a Pod to be given a Qos of BestEffort, the container in the Pod must not have any memory or CPU limits or requests.

`Burstable`: The Pod does not meet the criteria for QoS class Guaranteed, At least one Container in the Pod has a memory orr CPU request 

`Guaranteed`: Every Container in the Pod must have CPU limit and a CPU request, and they must be same, Every Container in the Pod must have a memory limit and a memory request , and the must be the same. 

# 要点
*Request*： 容器使用的最小资源要求，不限制容器的最大可使用资源。

*Limit*： 容器能使用资源的资源的最大值，设置为0表示使用资源无上限。


>  Memory目前只支持Request，Limit必须强制等于Request，这样确保容器不会因为内存的使用量超过了Request但没有超过Limit的情况下被意外的Kill掉

如果仅仅容器的内存使用量超过了Request但没有超过Limit的情况下，容器是不会被Kill掉的，所以上面这句话中”容器被意外的Kill掉“是其他原因导致的。比如出现内存资源抢占时。

# Kubernetes 中资源的抢占

## 可压缩资源的抢占策略 
--- 按照Request的比值进行分配

## 不可压缩资源的抢占策略
按照优先级的不同，进行Pod的驱逐。

优先级？详细官网说明：[Evicting end-user Pods](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/#evicting-end-user-pods)  

1. Request=Limit=0
2. 0 < Request < Limit < Infinity
3. 0 < Request==Limit

> 由于对不可压缩的资源，发生抢占的情况会出Pod被意外Kill掉的情况，所以建议对于不可以压缩的资源(Memory, Disk) 的设置为0<Requst==Limit

# 参考

1. Kubernetes 资源分配之Request和Limit解析
  https://cloud.tencent.com/developer/article/1004976

2. Configure Quality of Service for Pods 
  https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/

3. Kubernets 针对资源紧缺处理方式的配置（有点过时）
  https://www.kubernetes.org.cn/1150.html


<br>

<center>  ·End·  </center>
