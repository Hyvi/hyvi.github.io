---
layout: post
title: "从Jekyll到hugo, 迁移Github Pages"
description: ""
categories: 
 - Daily
tags: 
- 日记
---

## 背景  
观察到一些技术blog把评论和github issue同步了(gitalk)，这个很赞。  
于是想在jekyll搭建的blog下增加这种评论，按照教程操作。理应是一两个小时的事情，而因为GWF和Mac下Ruby环境的折腾一个大晚上。  
一觉后，不应浪费时间在这些网络问题上，blog主要是思考、怎么写、怎么表达。  
于是选择hugo来迁移Blog。    

## 实践  
完全参考 [使用 Hugo + GitHub Pages 搭建个人博客](https://mogeko.me/2018/018/)   
连风格也完全一(lan)样(ren)。。。  
一天搭建完  

## 后续  
hugo有很多有趣的功能，比如shortcode, 前段时间一直想通过shortcode让blog支持流程图和思维导图  
**好处**  

* 现有的工具(xmind, 百度脑图等)生成，然后导出图片, 若更新图中内容时会比较麻烦.  
  目前想到简单的办法是将xmind的源文件和图片同名保存, 更新图片内容，更新源文件的同时，导出同名的图片并覆盖.  

**坏处**  

* 如果后续迁移到其他Blog架构，会出现因为不支持shortcode显示导致页面显示流程的代码。  

结论：能不用shortcode的情况，换其他表达方式。  
