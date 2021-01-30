---
title: "Prometheus Practise"
date: 2020-11-06T20:00:52+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
## 背景
为什么要自建 Promethues, 云服务商提供的挺好的。

## 名词解释 
刚接触, 还是很多新词汇

| 名词 |解释|
|---|---|
|Exportor|用于向Prometheus Server暴露数据采集的endpoint，Prometheus轮训这些Exporter采集并且保存数据；|
|ServiceMonitor| a ServiceMonitor describes the set of targets to be monitored by prometheus. |
|Prometheus Operator| 简单运行 Promethues 在 kubernetes 上，并保持 Kubenetes 本土化的配置选项。[Prometheus operator design](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/design.md) |

### Operator 

An Operator is an application-specific controller that extends the kubernetes API to  create , configure, and manage instances of complex stageful applications on behalf of a kubernetes user. 

it builds upon the basic kubernetes resource and controller concepts but includes domain or application-specific knowledge to automate common taks.

![](https://coreos.com/sites/default/files/inline-images/Overview-etcd_0.png)

An  Operator is  software that encodes this domain knowledge and extends the kubernetes API through the third party resources mechanism, enabling users to create, configure, and manage applications. 

 Operator 与 Controller 区别在于：<br /> a Controller with the following characteristics qualify as an operator : <br /> 1. Contains workload-specific knowledge <br /> 2. Manages workload lifecycle <br /> 3. Offers a CRD

## 监控指标 
GPU Grafana 面板配置： [GPU NODES V2](https://grafana.com/grafana/dashboards/11752)

|指标|说明|
|---|---|
|DCGM_FI_DEV_FB_USED | GPU 已用显存 | 
|DCGM_FI_DEV_FB_FREE | GPU 未用显存 |
|DCGM_FI_DEV_GPU_UTIL | GPU 使用率 |


## 开始



## 有感

- K8s CRD 无处不在

## FAQ 
1. DCGM_FI_DEV_FB_FREE 数值和实际的内存对不上的？
    - A: 使用的型号是T4系列，具体的型号是 [ecs.gn6i-c16g1.4xlarge](https://www.alibabacloud.com/help/zh/doc-detail/108496.htm?#title-n0p-6ch-ma3), GPU 显存为 16G， 系统内存为 12G。而 NVIDIA dcgm-exporter 中监控的指标 DCGM_FI_DEV_FB_USED 为 GPU 显存大小，系统的内存通过 node_memory_MemTotal_bytes、node_memory_Buffers_bytes、node_memory_Cached_bytes、node_memory_MemFree_bytes 指标（来自 [GPU NODES V2](https://grafana.com/grafana/dashboards/11752) ) 来监控.
    - A: 当在 GPU 环境下提到内存时，须要区分下说的是 GPU 显存还是系统内存。

## 参考

[Introducing Operators : Putting Operational Knowledge into Software .](https://coreos.com/blog/introducing-operators.html)

[Promethues Operator User Guide](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/user-guides/getting-started.md)

Controllers and Operators, https://octetz.com/docs/2019/2019-10-13-controllers-and-operators/

[Promethues Book 中文 ](https://yunlzheng.gitbook.io/prometheus-book/)

[NAIDIA GPU monitoring tools on Linux](https://github.com/Hyvi/gpu-monitoring-tools)


[Integrating GPU Telemetry into Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/kubernetes/dcgme2e.html)

[Promethues 动态发现 Target 和 Relabel 的应用](https://blog.csdn.net/M2l0ZgSsVc7r69eFdTj/article/details/79124770)


[GPU-Nodes-Metrics 12027 设置](https://blog.csdn.net/u010953692/article/details/107143338)

<br>

<center>  ·End·  </center>
