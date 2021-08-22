---
title: "Bigdata Arch"
date: 2020-03-16T23:45:29+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

## 背景

## 行业案例

### 腾讯游戏大数据应用
[大数据背后的价值 - 腾讯游戏大数据应用](https://pan.baidu.com/disk/home#/all?vmode=list&path=%2F0%20%E6%9E%B6%E6%9E%84%E5%A4%A7%E4%BC%9A%E8%B5%84%E6%96%99%2FArchSummit%202015%20shenzhen%2F%E5%A4%A7%E6%95%B0%E6%8D%AE%E8%83%8C%E5%90%8E%E7%9A%84%E4%BB%B7%E5%80%BC%E4%B8%93%E9%A2%98)   

- 大数据落地应用 = 数据 + 系统 + 算法 + 应用场景
- 腾讯游戏用户数据分层体系
- 腾讯游戏数据处理系统架构 

### 饿了么数据仓库治理及数据应用

[大数据背后的价值 - 饿了么数据仓库治理及数据应用 ]( https://pan.baidu.com/disk/home#/all?vmode=list&path=%2F0%20%E6%9E%B6%E6%9E%84%E5%A4%A7%E4%BC%9A%E8%B5%84%E6%96%99%2FArchSummit%202015%20shenzhen%2F%E5%A4%A7%E6%95%B0%E6%8D%AE%E8%83%8C%E5%90%8E%E7%9A%84%E4%BB%B7%E5%80%BC%E4%B8%93%E9%A2%98 )   

#### 数据仓库的建设  
##### 标准化和规范化 
##### 统一日志搜集框架 
#### 原则

- 主题划分
- 数据一致性
- 维度建设 

#### TODO 

- 数据权限管理
- 数据使用记录
- 数据开放平台

## 存储读取/写入

[Data Lake  系列： 关于 EMRFS S3 优化的提交程序，你了解吗](https://zhuanlan.zhihu.com/p/113892824) 文章与 FileOutputCommitter 进行了比较。 

同时在 [github repo s3committer](https://github.com/rdblue/s3committer) 引出了 [ multi-part upload API ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html) 技术，可以用于处理大文件上传慢的问题。

但是对于小文件上传问题， 是否可以就并发上传就行了呢？ No

方案： 压缩上传，上传完成后通过 `AWS Lambda` 来解压缩。 其中通过流（Stream）的方式解决 *Only 500MB of disk space per instance* 的限制<sup>[1]</sup>，但执行时间有15分钟的限制，对于超大文件还是有。



## 参考 

[1] John Paul Hayes: How to extract a HUGE zip file in an Amazon S3 bucket by using AWS Lambda and Python

<br>

<center>  ·End·  </center>
