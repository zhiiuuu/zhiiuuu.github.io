---
layout: post
title: base64 session cookie JWT
date: 2019-11-04
categories: test
tags: token

---

# base64 session cookie JWT

base64是网络上最常见的用于传输8bit字节码的编码方式之一.常见 url

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

