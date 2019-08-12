---
layout: post
title: JavaScript
date: 2019-07-24
categories: test
tags: JavaScript
---

# JavaScript

- `<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>`

- js是属于HTML和Web的编程语言
- 在js 中函数是对象方法
- call():方法重用,可以编写能够在不同对象上使用的方法
- typeof()返回的数据类型
  - string
  - boolean
  - number
  - undefined
  - function
  - object
    - array
    - null
    - object
- 判断是否是数组
  - arr.constructor == true/false
  - 使用call()方法
- js地址引用和值引用
  - 数字/字符串/布尔类型的为原始类型,是值引用
  - 数组/对象类型为地址引用

#### 何为作用域

- 简单的说:js的作用域是靠函数来形成的,也就是说一个函数的变量在函数外不可以访问.

#### 少传参数

- 当函数中用不到第三个参数的时候可以只传两个参数,但是当一个函数有3个参数,而调用这个函数的时候只给它传两个参数,第三个参数的值默认为undefined

#### 垃圾回收器

- javascript使用垃圾回收机制来自动管理内存.垃圾回收是一把双刃剑,其好处是可以大幅简化程序的内存管理,降低程序员的负担,减少因长时间运转而带来的内存泄露问题.但使用了垃圾回收即意味着程序员将无法掌控内存.ECMAScript没有暴露任何垃圾回收器的接口.我们无法强迫其进行垃圾回收,更无法干预内存管理

#### 执行上下文

- 当函数执行时,会创建一个称为执行上下文的内部对象(可理解为作用域).一个执行上下文定义了一个函数执行时的环境
  - 创建作用域链
  - 创建变量对象(函数的形参/函数声明/变量声明)
  - 求this的值

#### instanceof

```
语法:object instanceof constructor

注意左侧必须是对象（object），如果不是，直接返回false，具体见基础类型。

基础类型

let num = 1

num instanceof Number // false

num = new Number(1)

num instanceof Number // true

明明都是num，而且都是1，只是因为第一个不是对象，是基本类型，所以直接返回false，而第二个是封装成对象，所以true。
```





