---
title: javaScript中is-not-defined,undefined和null的区别
date: 2017-04-26 11:17:07
tags: [javascript, undefined ]
categories: javaScript
---
# is not defined与undefined
之前没太注意is not defined和undefined有什么区别,每次都是简单的把两者理解为**未定义**,现在回过头来梳理js基础的时候才发现其中区别还是很鲜明的。
先从单纯的字面意思来理解一下（有道词典）：
> is not defined: 未定义
>
> not defined: 未定义,没有定义,无法定义


<!-- more -->
&&
> undefined: 不明确的
单从字面意思大体也能看出两者的区别:前者是没有定义，也就是说没有;后者是不明确的,也就是说不知道有没有定义.
## not defined
看demo1:

```
console.log(a)  
// 报错:a is not defined  终止运行
```
> 一个**未定义** 的变量是**没有声明**的变量,这样的变量在使用时会直接报错误。

## undefined
#### 一个定义了但未赋值的 **变量**
demo2:
```
var a
console.log(a)  
// 未报错,提示: undefined
```
#### 一个定义了但把值赋为undefined的 **变量**
demo3:
```
var p = 1
p = undefined
console.log(p)  
// 未报错,提示: undefined
```
#### 一个对象没有赋值的属性
demo4:
```
console.log(window.a)
// 未报错,提示: undefined
```
demo5:
```
var a = []
console.log(a.b)
// 未报错,提示: undefined
```
demo6:
```
var a = {}
console.log(a.b)
// 未报错,提示: undefined
```
#### 一个没有返回值的函数
demo7:
```
function f() {console.log(1)}
console.log(f())
// 未报错,提示: undefined
```

> 有一点需要注意的是not defined 和 undefined 的typeof()的值都为"undefined",所以无法用typeof()来判断这两者。

# undefined 与 null
## 两者相同--在if语句里都被解析为false
demo8:
```
!undefined ? console.log('undefined is false') : console.log('undefined is not false')
// undefined is false  
```
demo9:
```
!null? console.log('null is false') : console.log('null is not false')
// null is false
```

## 用法的不同
虽然null和undefined基本是同义的，但是在用法上还是有一些细微的差别的

#### null
null表示“没有对象”,即此处不该有值
1. 作为函数的参数，表示该函数的参数不是对象。
2. 作为对象原型链的终点。
demo10:
```
Object.getPrototypeof(object.prototype)
// null
```
## undefined
如上文demo2-demo7 部分
