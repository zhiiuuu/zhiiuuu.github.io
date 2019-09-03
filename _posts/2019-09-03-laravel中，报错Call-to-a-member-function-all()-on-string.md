---
layout: post
title: laravel中，报错Call to a member function all() on string
date: 2019-09-03
categories: test
tags: NOTE
---

# laravel中，报错Call to a member function all() on string

**报错如下：**

ErrorException thrown with message "Call to a member function all() on string (View: D:\code\blog\resources\views\admin\pass.blade.php)"



**解决：在**pass.blade.php文件里，做一个判断，

代码如下：

​          @if(count($errors)>0)

​                **@if(is_object($errors))**

​                     @foreach($errors->all() as $error)

​                       {{$error}}

​                       @endforeach

​                    **@else**

​                         **{{$errors}}**

​                    **@endif**   

​            @endif

**原因：**

**修改密码时，后台写的错误信息$errors，可能是一个对象（正确）代码如：**

**return back()->withErrors($validator);**

**，也可能是一个字符串（报错，因为字符串，不能执行：$errors->all()方法），代码如：**

**return back()->with('errors','原密码不正确');**