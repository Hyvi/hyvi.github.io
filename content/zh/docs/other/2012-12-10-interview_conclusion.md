---
layout: post
title: "INTERVIEW CONCLUSION"
description: "2012-12-08 福田财富大厦 问题"
categories: 
- Tech
tags: ["interview"]
---
 

### 10万数字，选取最大的100个数。算法度
这个题目当时没细想，估计面试官想问排序问题，然后说了下快速排序。<br />
其实完全没必要排序。遍历一次就可找出来最大的100数字。 

类似问题： [Write a program to find 100 largest numbers out of an array of 1 billion numbers](https://stackoverflow.com/questions/19227698/write-a-program-to-find-100-largest-numbers-out-of-an-array-of-1-billion-numbers) 


### xxxx年xx月xx日 xx:xx:xx 表示当前日期
[代码](http://codepen.io/Hyvi/pen/BheHd) 终于重写到自己感觉满意了。

### 给定个返回json的url，有哪些方法获取数据然后显示在其他域的页面上
- 如果提供jsonp的调用,页面中调用jsonp方式
- 后端代理的方式。
- Cross-domain Request(cors)
- 还有其他的方式吗？ Tell me!!!


## 算法时间复杂度与空间复杂度的计算

**时间频度**

一个算法所花费的时间与代码语句执行的次数成正比。我们把一个算法中的语句执行次数称为时间频度，记作 T(n)

**渐进时间复杂度**

在时间频度 T(n) 中，n 表示着问题的规模，当 n 不断变化时， T(n) 也会不断地随之变化。那么，如果我们想知道 T(n) 随着 n 变化时会呈现什么样的规律，那么就需要引入时间复杂度的概念。

如果存在某个函数 f(n)， 使得当 n 趋于无穷大时，T(n)/f(n)的极限值是不为零的常数，那么 f(n) 是 T(n) 同数量级的函数，记作 T(n) = O(f(n))，称 O(f(n)) 为算法的渐进时间复杂度，简称为时间的复杂度。 

常见的时间复杂度有： O(1) 常数型； O(log<sub>n</sub>) 对数型；O(n) 线性型；O(nlog<sub>n</sub>) 线性对数型；O(n<sup>2</sup>) 平方型；O(n<sup>3</sup>) 立方型；O(n<sup>k</sup>) k次方型；O(2<sup>n</sup>) 指数型。

更多时间复杂度实例<sup>[1]</sup>


## 参考
[1] 程序新视界: [LeetCode0：学习算法必备知识：时间复杂度与空间复杂度的计算](https://cloud.tencent.com/developer/article/1769988)

