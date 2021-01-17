---
layout: post
title: "Python 面试Problems"
description: ""
categories: ['Tech']
tags: ['interview','python']
---
 
[Python面试必须要看的15个问题](http://codingpy.com/article/essential-python-interview-questions/)  
  
* 到底什么是Python? //考察语言特性
* 补充缺失的代码

```python 
def print_directory_contents(sPath):
    """
    这个函数接受文件夹的名称作为输入参数，
    返回该文件夹中文件的路径，
    以及其包含文件夹中文件的路径。

    """
    # 补充代码
```

* 你如何管理不同版本的代码？
* 下面代码会输出什么：

```python 
def f(x,l=[]):
    for i in range(x):
        l.append(i*i)
    print l

f(2)
f(3,[3,2,1])
f(3)
```

* 这两个参数是什么意思：*args，**kwargs？我们为什么要使用它们？
* 下面这些是什么意思：@classmethod, @staticmethod, @property？
* 递归和生成器（generator）的使用
* 简要描述Python的垃圾回收机制（garbage collection）。
* 将下面的函数按照执行效率高低排序。它们都接受由0至1之间的数字构成的列表作为输入。这个列表可以很长。一个输入列表的示例如下：[random.random() for i in range(100000)]。你如何证明自己的答案是正确的。

```python 

def f1(lIn):
    l1 = sorted(lIn)
    l2 = [i for i in l1 if i<0.5]
    return [i*i for i in l2]

def f2(lIn):
    l1 = [i for i in lIn if i<0.5]
    l2 = sorted(l1)
    return [i*i for i in l2]

def f3(lIn):
    l1 = [i*i for i in lIn]
    l2 = sorted(l1)
    return [i for i in l1 if i<(0.5*0.5)]
		
```

