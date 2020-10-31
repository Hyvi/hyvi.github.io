---
title: "Monorepo for Golang With Bazel"
date: 2020-10-31T14:39:06+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

# 背景

> ProtocolBuffer + gRPC + Bazel + Monorepo + Microservice is the common poly glot pattern which is also used in Google and other tech companies

微服务面临的问题是大量的 repo（成百上千）， 尤其在依赖库的管理、规范的落地，非常麻烦困难。

需求点
- 使用同一的 go.mod 来管理依赖
- 在不同的应用里可以服用共同的代码块
- 可以执行单个应用的测试也可以执行所有应用的测试
- 可以构建单个应用或者所有的应用

# 实践 
《Create Go Monorepo with Go-modules and Bazel》

Example: https://github.com/PxyUp/go_monorepo 

疑惑点：
- 每个 module 需要写 BUILD.bazel 配置文件，带来额外的麻烦。
- 如何跟 reviewdog(golangci-linter) 结合
- 不支持 IDE， 给习惯用 IDE 的来说是不愿意的接受
- 如何处理 Grpc 生成的代码

# 结论
- 利于代码共享，解决各自孤立的状态
- 利于统一依赖库，统一升级，确保安全。
- 新的技术，激活技术氛围和兴趣

# 参考
[Bazel 结合 golangci-linter](https://github.com/atlassian/bazel-tools)

[Guide: Create monorepo with Go Modules and Bazel](https://www.reddit.com/r/golang/comments/dfod3o/guide_create_monorepo_with_go_modules_and_bazel/) 

[Monorepo at Uber](https://www.reddit.com/r/golang/comments/gjo2ei/building_ubers_go_monorepo_with_bazel/)

<br>

<center>  ·End·  </center>
