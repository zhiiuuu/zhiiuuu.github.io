---
layout: post
title: react map循环一直报Expected to return a value in arrow function array-callback-return警告
date: 2020-04-04
categories: test
tags: React

---

# react map循环一直报Expected to return a value in arrow function array-callback-return警告

react map循环一直报Expected to return a value in arrow function array-callback-return警告，提示内容的意思是没有return一个值

**解决办法就是：**

1：用Object.keys(this.props.ntn).forEach去替换.map，因为ESLint [array-callback-return](http://eslint.org/docs/rules/array-callback-return)这个警告是因为在使用**map, filter , reduce** 没有去返回一个值。

2：**当然也可以使用map,在react中用jsx的方式，直接把{}改成()即可。**