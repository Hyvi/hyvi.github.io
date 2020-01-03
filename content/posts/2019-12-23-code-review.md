---
title: "Code Review 开始"
date: 2019-12-23T20:27:25+08:00
draft: false
tags: 
- 管理
categories: 
- Tech 
featured_image: 
description: 
---
# 简介 
整个golang团队20多人，没有code review ，对项目质量、对结果产出、对新人的成长，对团队交流的氛围影响大。 看过[Google 代码评审规范](https://www.infoq.cn/article/QJi1Kqm4pH3UNAqNzl3l)，解决了我之前一些疑问和也让我坚定的去Code Review。  
当没有code review时候，要求重构，而重构价值是释放历史包袱，并没有产生任何其他价值  

- 我们的提交是这样的  

```golang
3b8e45c - Slove Confilct -  2 weeks ago -
0a39ecd - FIXS: vendor -  2 weeks ago -
7817d14 - debug -  2 weeks ago -
67539e2 - debug -  2 weeks ago -
9044356 - Slove Confilct -  2 weeks ago -
d47db91 - FIXS: ss -  2 weeks ago -
8913c30 - Slove Confilct -  2 weeks ago -
2d407d2 - FIXS: logger -  2 weeks ago -
```

``` golang
b9af055 - 打印日志 -  7 weeks ago - 
1124e92 - 打印日志 -  7 weeks ago - 
88d0eac - 修改log -  7 weeks ago - 
ad0b3dd - 修改日志 -  7 weeks ago - 
4aa0740 - 答应日志 -  7 weeks ago - 
824658a - 修改日志 -  7 weeks ago - 
178c30c - 打印日志 -  7 weeks ago - 
```
> 在pull request的时候，认真review下所有的commit，该合并得合并，该修改得修改

- 我们的命名是这样的  
  这里不截图纪念了. 

- 我们的代码分支和发版是这样的  
  本地打包,更恶心的是代码不提交本地打包的.  

- 我们的单元测试是这样的  
  几乎没有  

我们开始要做Code Review， 从哪里开始了？  
# 方式
谁对谁在什么时候用什么方式去做什么？

## 第一个“谁”
如果项目存在两人或者两人以上开发 

- 如果开发提交代码，则应用项目负责人  
- 如果应用负责人也参与开发，则由另外任一一位开发做一次review，然后上一级的负责人做第二次review。 

如果应用负责人和开发是同一个人，这时候为“小组Leader”   

## 第二个“谁”
业务开发人员对应用提交的pull request 

## 什么时候
提交Review时的当天或者第二天须完成

## 什么方式
依照代码审核规范， 目前缺少自己的审核规范，参考[Google 代码评审规范](https://www.infoq.cn/article/QJi1Kqm4pH3UNAqNzl3l)，必须熟读

## 做什么
阅读提交的代码并给出建议完成审核



<br>

<center>  ·End·  </center>