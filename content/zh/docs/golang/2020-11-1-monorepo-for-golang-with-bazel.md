---
title: "Monorepo for Golang With Bazel"
date: 2020-10-31T14:39:06+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

## 背景

> ProtocolBuffer + gRPC + Bazel + Monorepo + Microservice is the common poly glot pattern which is also used in Google and other tech companies

微服务面临的问题是大量的 repo（成百上千）， 尤其在依赖库的管理、规范的落地，非常麻烦困难。

需求点
- 使用同一的 go.mod 来管理依赖
- 在不同的应用里可以服用共同的代码块
- 可以执行单个应用的测试也可以执行所有应用的测试
- 可以构建单个应用或者所有的应用

## 新概念

### Bazel
> Bazel is an open-source build and test tool similar to Make, Maven, and Gradle. 
> It uses a human-readable, high-level build language. 
> Bazel supports projects in multiple languages and builds outputs for multiple platforms.
> Bazel supports large codebases across multiple repositories, and large numbers of users.

### Rule 
>A rule defines a series of actions that Bazel performs on inputs to produce a set of outputs.

rule_go 为 golang 编写的 rules。

对 Rule 进一步的了解，学习如何编写 rule，资料入口：rule_go 的作者系列文档： [A simple set of Go rules for Bazel, used for learning and experimentation.](https://github.com/jayconrod/rules_go_simple)

#### repository rule 
解决依赖于安装在本机上的 toolchain，这样如果不同的开发者需要在本地上安装 toolchain。 
一旦 toolchain 不一样的时候，构建出来的结果不一样。于是，通过 repository rule 来下载 go toolchain 和生成 custom build file. 

a repository rule, a special function that can be used in a WORKSPACE file to define an external WORKSPACE.

### Gazelle 
> Gazelle is a build file generator for Bazel projects. It can create new BUILD.bazel files for a project that follows language conventions,
> and it can update existing build files to include new sources, dependencies, and options. Gazelle natively supports Go and protobuf, 

## 实践 
《Create Go Monorepo with Go-modules and Bazel》

Example: https://github.com/PxyUp/go_monorepo 

给 go-present 仓库加上 bazel 构建 monorepo 仓库管理方式

### Gazelle 使用
```
bazel run //:gazelle
```

疑惑点：

- [x] 每个 module 需要写 BUILD.bazel 配置文件，带来额外的麻烦。
    - Gazelle build file generator，原生支持 Go / protobuf
- 如何跟 reviewdog(golangci-linter) 结合
- [x] ~~不支持 IDE， 给习惯用 IDE 的来说是不愿意的接受~~
- 如何处理 grpc 生成的代码
    - 共享生成的仓库

## 结论
- 有利于代码共享，解决各自孤立的状态
- 有利于统一依赖库，统一升级，确保安全。
- 新的技术，激活技术氛围和兴趣

## FAQ 
Q: how do you set up a CI/CD pipeline for a mono repo? When a code change to the repository triggers CI

A: http://blog.shippable.com/ci/cd-of-microservices-using-mono-repos， 更多内容参考： https://github.com/korfuri/awesome-monorepo/blob/master/README.md

## 参考
[Bazel 结合 golangci-linter](https://github.com/atlassian/bazel-tools)

[Guide: Create monorepo with Go Modules and Bazel](https://www.reddit.com/r/golang/comments/dfod3o/guide_create_monorepo_with_go_modules_and_bazel/) 

[Monorepo at Uber](https://www.reddit.com/r/golang/comments/gjo2ei/building_ubers_go_monorepo_with_bazel/)

[cmake + Conan：decentralized and multi-platform package manager to create and share all your native binaries.](https://conan.io/)

[Monorepo with bazel and go module： 践行者](https://hardyantz.medium.com/)

<br>

<center>  ·End·  </center>
