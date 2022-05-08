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

<center>  ·End·  </center>
