---
title: "Prometheus Practise"
date: 2020-11-06T20:00:52+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
# 背景
为什么要自建 Promethues, 云服务商提供的挺好的。

# 名词解释 
刚接触, 还是很多新词汇

| 名词 |解释|
|---|---|
|Exportor|用于向Prometheus Server暴露数据采集的endpoint，Prometheus轮训这些Exporter采集并且保存数据；|
|ServiceMonitor| a  ServiceMonitor describes the set of targets to be monitored by prometheus |
|Prometheus Operator| 简单运行 Promethues 在 kubernetes 上，并保持 Kubenetes 本土化的配置选项|

# 监控指标 
|指标|说明|
|---|---|
|DCGM_FI_DEV_FB_USED | GPU 已用内存 | 
|DCGM_FI_DEV_FB_FREE | GPU 未用内存 |
|DCGM_FI_DEV_GPU_UTIL | GPU 使用率 |

# 开始



# 有感

- K8s CRD 无处不在


# 参考

[Promethues Operator User Guide](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/user-guides/getting-started.md)

[Promethues Book 中文 ](https://yunlzheng.gitbook.io/prometheus-book/)

[NAIDIA GPU monitoring tools on Linux](https://github.com/Hyvi/gpu-monitoring-tools)


[Integrating GPU Telemetry into Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/kubernetes/dcgme2e.html)

[Promethues 动态发现 Target 和 Relabel 的应用](https://blog.csdn.net/M2l0ZgSsVc7r69eFdTj/article/details/79124770)


[GPU-Nodes-Metrics 12027 设置](https://blog.csdn.net/u010953692/article/details/107143338)

<br>

<center>  ·End·  </center>
