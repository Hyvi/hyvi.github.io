---
title: "Golang Pprof 使用梳理"
date: 2020-04-16T09:11:28+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
# 背景
当前碰到的问题： 

- 部分服务CPU负载比较高
- 服务内存使用量比较大
- 服务高延迟（内存CPU负载都不高情况）

golang开发中有一些定位这些问题的套路和工具，在本文中汇总，记录并不断改进解决问题的思路。

从两个方面考虑： 

- 系统监控统计级别数据指标
    - goroutine数量
    - 堆(heap)内存使用量
    - 栈(stack)内存使用量
    - 其他...(待补充）
- 问题定位所需的详细数据
    - 获取系统实时堆内存分配详细信息: 具体到这个内存在哪里分配的。
    - 获取系统实时所有goroutine调用堆栈信息: 具体到这个goroutine是在哪里启动的，以及当前在干什么
    - 获取系统实时堆内存调优辅助统计信息： 具体是在哪里分配了多少内存，以及TOP N分别是哪些，甚至是每个内存分配的来源图
# pprof

## 获取系统实时堆内存分配详情
``` golang 
//引入pprof
import "net/http/pprof"
//在http router上加入
this.debugMux.HandleFunc("/debug/pprof/", http.HandlerFunc(pprof.Index))
``` 

`curl -XGET "http://192.168.149.150:8080/debug/pprof/heap?debug=2"` 获取heap内存的详细信息，其中8080是你开启的http server的端口，debug=2意味着需要输出详细信息

## 获取系统实时所有goroutine调用栈信息
通过`curl -XGET "http://192.168.149.150:8080/debug/pprof/goroutine?debug=2"`拿到的就是goroutine的详细信息

## 获取系统实时堆内存调优辅助统计信息 
`go tool pprof -inuse_space http://192.168.149.150:8080/debug/pprof/heap`，进入pprof交互模式后，可以通过top, tree等进一步查看统计信息，同时，也可以通过png命令，将内存信息输出成图片，以图片的形式显示内存的分配、占用情况

## 获取 trace 数据
通过：`curl -XGET "http://127.0.0.1:8080/debug/pprof/trace?seconds=30" -o 002_trace_2017_09_08.out`我们将获取一个30秒的trace数据(trace_02.out)，通过`go tool trace 002_trace_2017_09_08.out`

## cpuprofile
侧重于统计程序各goroutine自身的运行状况，更加适用于分析针对cpu密集型逻辑导致的latency过高问题

# 参考
1. go tool proof 郝琳的中文说明 #TODO
  https://github.com/hyper0x/go_command_tutorial/blob/master/0.12.md 

2. Profiling Go Programs 官方Blog #TODO
  https://blog.golang.org/pprof

3. 一次 Golang 程序内存泄漏分析之旅
  http://lday.me/2017/09/02/0012_a_memory_leak_detection_procedure/ 链接访问有点问题，可以用google cache查看文字

4. 一次 Golang 程序延迟过大问题的定位过程
  http://lday.me/2017/09/13/0013_a_latency_identification_procedure/



<br>

<center>  ·End·  </center>
