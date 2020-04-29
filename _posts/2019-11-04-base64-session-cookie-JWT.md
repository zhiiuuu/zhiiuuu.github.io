---
layout: post
title: base64 session cookie JWT
date: 2019-11-04
categories: test
tags: token

---

# base64 session cookie JWT

base64是网络上最常见的用于传输8bit字节码的编码方式之一.常见 url Base64就是一种基于64个可打印字符来表示二进制数据的方法

### UUID与Base64

让我们以base64表示法开始 每个字节的基数为64(六十四进制) 因此在3个字节在base64中需要 来表示2个字节的实际值 一个UUID的值由16个字节的数组组成 如果我们除以3 则余数为1 为处理该问题 base64编码在末尾添加了"=="

Base64要求把每三个8Bit的字节转换为四个6Bit的字节（3*8 = 4*6 = 24），然后把6Bit再添两位高位0，组成四个8Bit的字节，也就是说，转换后的字符串理论上将要比原来的长1/3

seesion与cookie是同时存在的 cookie保存着session id

### JWT原理

1. 服务端 有自己的一个字符串 str_a

2. 用户登录成功 

   ```
   {name:'name',user_id:1,expiration:'2019-01-01'} 需要返回给客户端的字符串 str_b
   ```

3. 加密两个字符串 md5(str_b+str_a) 得到新的字符串str_c

4. 返回给客户端 

   ```
   {name:'name',user_id:1,expiration:'2019-01-01'}+str_c
   ```

### 验证JWT

客户端下一次请求时 就带着`{name:'name',user_id:1,expiration:'2019-01-01'}+str_c`

服务器截取``{name:'name',user_id:1,expiration:'2019-01-01'}`与自己的str_a组合 用自己的加密方式加密 看是否等于str_c 就可以了

> 优点:不用保存到数据库
>
> 缺点:不能给用户做过期操作 只能等他自己过期

