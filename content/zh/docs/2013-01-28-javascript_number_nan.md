---
layout: post
title: " javascript Number --- 再次结识"
description: "2013-01-27 javascript基本功"
categories: 
- Tech
tags: ["javascript"]
---
 


javascript类型划为两大类：原始类型（甭管这样的翻译是否规范，英文为primitive type) 和 对象类型。原始类型又划为四大类：数值、字符串、布尔值，还有两个特殊的类型：null 和 undefined 。 
废话少说，直接进入主题：*javascript number的几点*
1. 与其他语言相比，javascript number不同点
>JavaScript does not make a distinction between integer values
>and floating-point values. All numbers in JavaScript are represented as floating->point values.

2. javascript number表达的数值是有限的，于是就有overflow, underflow。
> Arithmetic in JavaScript does not raise errors in cases of overflow, underflow, or division by zero.
> (-)Infinity when overflow, (-)0 when underflow 
> Division by zero is not an error in JavaScript: it simply returns infinity or negative
infinity.

3. javascript number 中特殊的NaN 
>There is one exception, however: zero divided by zero does not have a well-defined value, and the result of this operation is the special not-a-number value, printed as  NaN.  NaN  also arises if you attempt to 
>* divide infinity by infinity
>* take the square root of a negative number
>* use arithmetic operators with non-numeric operands that
>cannot be converted to numbers

<pre><code>
	Infinity // A read/write variable initialized to Infinity.
	Number.POSITIVE_INFINITY // Same value, read-only.
	1/0 // This is also the same value.
	Number.MAX_VALUE + 1 // This also evaluates to Infinity.
	Number.NEGATIVE_INFINITY // These expressions are negative infinity.
	-Infinity
	-1/0 
	-Number.MAX_VALUE - 1
	NaN // A read/write variable initialized to NaN.
	Number.NaN // A read-only property holding the same value.
	0/0 // Evaluates to NaN.
	Number.MIN_VALUE/2 // Underflow: evaluates to 0
	-Number.MIN_VALUE/2 // Negative zero
	-1/Infinity // Also negative 0
	-0
</code></pre>
4. javascript NaN != NaN 
> The not-a-number value has one unusual feature in JavaScript: it does not compare equal to any other value, including itself. This means that you can’t write x == NaN to determine whether the value of a variable xis  NaN. Instead, you should write  x != x. That expression will be true if, and only if, x is NaN. The function isNaN()is similar. It returns trueif its argument is NaN, or if that argument is a non-numeric value such as a string or an object. The related function isFinite()returns trueif its argument is a number other than NaN, Infinity, or -Infinity.

5. .3-.2 == .1 & .2-.1 == .1 

6. -0 === 0 
<pre><code>
    var zero = 0; // Regular zero
    var negz = -0; // Negative zero
    zero === negz // => true: zero and negative zero are equal 
    1/zero === 1/negz // => false: infinity and -infinity are not equal
</code></pre>

这算是对之前文章http://hyvi.sinaapp.com/2012/10/09/javascript-nan/ 做了个补充。
twitter上的代码：
<pre><code>  
    [0,7,5,10,4,15,2,13,4,16,4,10,1].map(function(a){return this[a];},typeof("")+typeof(0)+NaN+"d.").join("") 
</code></pre>
