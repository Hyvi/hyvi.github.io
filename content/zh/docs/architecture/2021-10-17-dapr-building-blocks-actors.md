---
title: "Dapr Building Blocks Actors"
date: 2021-10-17T16:18:16+08:00
draft: true
---

## 简述
Dapr 的 Building Blocks 是为了提供在分布式下一些最佳实践的场景支持，方便开发者能快速进行业务开发。其中 Actors 为其中稍有的一种。 那 Actors 到底是什么，解决什么问题，原理是怎样的？ 

[OAM 详解]({{< ref "/zh/docs/k8s/2020-01-05-OAM.md">}})文章对 Actor Pattern 模式简单了解。在这里详细记录 actor 内容

## 名词解释

**partition**

为了提高可伸缩性和可靠性，在 Actor 服务的所有实例中进行分区。Dapr placement 服务负责跟踪分区信息<sup>[1]</sup>

![Actor placement service](https://docs.microsoft.com/en-us/dotnet/architecture/dapr-for-net-developers/media/actors/placement.png)

1. 在启动时，边车从 actor service 获取已注册的 actor type 以及 actor configuration settings

2. 边车将这些信息发送到 placement service 

3. placement service 广播已更新的分区信息，每个实例保存一份副本，用于后续调用 actors


## Actor lifetime
Actor 的创建、闲置超时、销毁。以及 reminder 对 Actor 的 lifetime 影响，而 Timer 没有影响。

## Actor reentrancy
A core tenet of the virtual actor pattern is the single-threaded nature of actor execution.

```
Actor A -> Actor A
ActorA -> Actor B -> Actor A
``` 

## Distribution and failover
The Dapr actor runtime manages distribution scheme and key range settings for you. This is done by the actor Placement service. `Actor placement service` 起到重要的作用。

## Actor communication
The Dapr actor runtime provides a simple **turn-based access mode** for accessing actor methods. 

在 preview feature 中，支持 Reentrancy （重入）

## Use vitual actors in Dapr

### Actor state management

为了使用 actors, state store 必须支持 multi-item transactions. 

## 参考

[1] 张善友：面向.NET开发人员的 Dapr- actors 构建块

[2] Microsoft： The Dapr actors building block
