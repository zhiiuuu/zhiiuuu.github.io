---
layout: post
title: varchar与char的区别
date: 2019-11-02
categories: test
tags: mysql

---

# varchar与char的区别

1、**CHAR**的长度是不可变的，而**VARCHAR**的长度是可变的，也就是说，定义一个CHAR[10]和VARCHAR[10],如果存进去的是‘ABCD’, 那么CHAR所占的长度依然为10，除了字符‘ABCD’外，后面跟六个空格，而VARCHAR的长度变为4了，取数据的时候，CHAR类型的要用trim()去掉多余的空格，而VARCHAR类型是不需要的。

2、**CHAR**的存取速度要比**VARCHAR**快得多，因为其长度固定，方便程序的存储与查找；但是CHAR为此付出的是空间的代价，因为其长度固定，所以难免会有多余的空格占位符占据空间，可以说是以空间换取时间效率，而VARCHAR则是以空间效率为首位的。

3、**CHAR**的存储方式是，一个英文字符（ASCII）占用1个字节，一个汉字占用两个字节；而**VARCHAR**的存储方式是，一个英文字符占用2个字节，一个汉字也占用2个字节。

4、两者的存储数据都是非unicode的字符数据。

