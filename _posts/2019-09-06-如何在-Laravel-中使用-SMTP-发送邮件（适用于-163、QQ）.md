---
layout: post
title: 如何在 Laravel 中使用 SMTP 发送邮件（适用于 163、QQ）
date: 2019-09-06
categories: test
tags: Laravel
---

# 如何在 Laravel 中使用 SMTP 发送邮件（适用于 163、QQ）

------

Laravel 提供了非常简单的邮件发送 API，但是文档却不是太清晰，再加上它采用传递闭包（回调函数）的方式调用，导致邮件发送的使用门槛偏高。

Laravel 4 和 Laravel 5 的邮件发送使用方式完全一致。Laravel 5 的邮件发送中文文档在：<http://laravel-china.org/docs/5.0/mail>

本文中，我将以 163 和 qq 邮箱为例，展示如何用 Laravel 内置的邮件发送类来发送邮件。

## 163邮箱的配置

修改邮件发送配置。修改以下配置：

### 1.163邮箱的配置项.env (就在主目录下)

```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.163.com
MAIL_PORT=25
MAIL_USERNAME=jhf123boy@163.com(填你自己的邮箱即可)
MAIL_PASSWORD=xxxxxxx(这里是你的授权码,不是你邮箱的密码)
MAIL_ENCRYPTION=
```

> 关于MAIL_PASSWORD配置项的说明
> 此项并不是作为发送邮件的代理邮箱的登录密码（也就是不是你邮箱的密码），而是开通smtp设置的授权码

![112](http://px6xvo4m7.bkt.clouddn.com/2019-09-07_095001.png)

## ![111](https://zhiiuuu.oss-cn-shanghai.aliyuncs.com/2019-09-07_095049.png?Expires=1567824772&OSSAccessKeyId=TMP.hVUtYw4bFk2s7D7jQBjjz7LtPEyoLkTjZwDk6VEdCtB4TQ1DjNxYHh5nVD18Dau5FT5yQXKRF4E1kdVPMyHf8Tt3h4J7cqctUkaA23LshvFV2AqaYdWT6kMHPaFGzV.tmp&Signature=GZphem6NHtsLqA1gU0Vg7NhrvGU%3D)

### 2.但是我们注意一下config/mail.php中有两项

```
'from' => [
        'address' => env('MAIL_FROM_ADDRESS', 'hello@example.com'),
        'name' => env('MAIL_FROM_NAME', 'Example'),
    ],
```

这里的MAIL_FROM_ADDRESS,MAIL_FROM_NAME在配置文件中是没有的。所以我们应该加到.env中

![](https://zhiiuuu.oss-cn-shanghai.aliyuncs.com/2019-09-07_095550.png?Expires=1567824931&OSSAccessKeyId=TMP.hVUtYw4bFk2s7D7jQBjjz7LtPEyoLkTjZwDk6VEdCtB4TQ1DjNxYHh5nVD18Dau5FT5yQXKRF4E1kdVPMyHf8Tt3h4J7cqctUkaA23LshvFV2AqaYdWT6kMHPaFGzV.tmp&Signature=lmSoj7BLNU5lb2xJzIe%2Bku8ANJs%3D)

### 3.控制器写法

email.active就是页面模板

![](https://zhiiuuu.oss-cn-shanghai.aliyuncs.com/markdown/2019-09-07_104313.png?Expires=1567827800&OSSAccessKeyId=TMP.hVUtYw4bFk2s7D7jQBjjz7LtPEyoLkTjZwDk6VEdCtB4TQ1DjNxYHh5nVD18Dau5FT5yQXKRF4E1kdVPMyHf8Tt3h4J7cqctUkaA23LshvFV2AqaYdWT6kMHPaFGzV.tmp&Signature=xssS5iMrSD96b%2B%2Bj3kerCDfNnyE%3D)

## qq邮箱的配置项



```
//smtp   协议MAIL_DRIVER=smtp//host   为smtp.qq.comMAIL_HOST=smtp.qq.com //端口   465MAIL_PORT=465//用户名 qq邮箱号MAIL_USERNAME=414582343@qq.com//密码   在qq邮箱的账户里面开启smtp后获得的授权码MAIL_PASSWORD=fhnjgraxnympcaga //加密   SSL(必填)MAIL_ENCRYPTION=SSL //发件地址 发件地址与用户名须一致MAIL_FROM_ADDRESS=414582343@qq.com//发件人MAIL_FROM_NAME=xiaohuazai
```

> 关于MAIL_PASSWORD配置项的说明
> 此项并不是作为发送邮件的代理邮箱的登录密码（也就是不是你邮箱的密码），而是开通smtp生成的授权码,生成授权码的步骤如下：

### 发送

在控制器或者模型里，调用以下代码：



```
$data = [
'email'=>$email, 
'name'=>$name,
'uid'=>$uid,
'activationcode'=>$code
];
Mail::send('activemail', $data, function($message) use($data){    
	$message->to($data['email'], $data['name'])->subject('欢迎注册我们的网站，请激活您的账号！');
});
```

邮件视图为 views/activemail.blade.php：



```
<!doctype html><html lang="zh-CN">  
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
</head><body>
<a href="{{ URL('active?uid='.$uid.'&activationcode='.$activationcode) }}" target="_blank">点击激活你的账号</a>
</body>
</html>
```