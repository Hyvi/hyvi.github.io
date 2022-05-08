---
title: "About Golang String"
date: 2022-05-08T09:11:28+08:00
draft: false
tags:
categories:
featured_image:
description:
---

## 问题

```golang
package main

import (
	"fmt"
)
func main() {
	var bys  [20]byte

	bys[0] =  'h'
	bys[1] =  'e'
	bys[2] =  'i'

	if string(bys[:]) == "hei" {
		fmt.Println("[20]byte('h','e','i') === \"hei\"")
	}
}
```
输出： [20]byte('h','e','i') === "hei"

## 要点

- the internal structure of any string type is declared like:

```golang
type _string struct {
   elements *byte // underlying bytes
   len      int   // number of bytes
}
```
- String types are all comparable, When comparing two strings, **their underlying bytes will be compared, one byte by one byte.**

- if one string is a prefix of the other one and the other one is longer, then the other one will viewed as the large one.

- when a byte slice is converted to a string, **the underlying byte sequence of the result string is also just a deep copy of the byte slice**.


## 延伸
```golang
package main

import (
	"fmt"
)

const s = "Go101.org"

// len(s) is a constant expression, 
// whereas len(s[:]) is not.
var a byte = 1 << len(s) / 128 
var b byte = 1 << len(s[:]) / 128

func main() {
	fmt.Println(a, b) // 4 0	
}

```

为什么会出现不一样的结果，一个要点是： **the special type deduction rule in bitwise shift operator operation** 

- 当位运算左元素为 **untyped value**， 并且右元素为 constant 时，运算的结果类型保持与左元素一样。

- 当位运算左元素为 **untyped value**， 并且右元素为 non-constant 时，首先左元素类型转化为 assumed type (it would assume if the bitwise shift operator operation were replaced by its left operand alone)

根据上面两个 rule, 上面语句变成：

```golang
var a = byte(int(1) << len(s) / 128)
var b = byte(1) << len(s[:]) / 128
```

<center>  ·End·  </center>
