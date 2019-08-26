---
layout: post
title: 利用cordova打包vue文件
date: 2019-08-26
categories: test
tags: Vue

---

# 利用cordova打包vue文件

## 1. 目前市场上流行的打包工具

1. 线上打包,也就是在线进行打包,其特点是打包简单,并且速度极快,缺点是:必须带有第三方的logo或者水印,比如:Hbuilder打包
2. 下线打包,分为普通的打包工具,和复杂的构建工具.普通的打包就是不含有自己的编辑逻辑,仅仅对项目进行打包,例如:cordova/create app ,复杂的构建工具包含了自己的语言逻辑和开发环境等等,例如:weex,react-native

## 2.使用cordova之前的准备工作

- 从硬件方法:

  - 如果你需要打包安卓,那么需要下载java环境
  - 如果你需要打包ios,那么需要mac电脑进行打包,并且电脑需要安装xcode

- 从软件方面

  - 首先,修改vue项目的index.html文件,在head中加入以下内容:(**如果添加了以下内容,你的页面样式会发生改变,那么只能不要添加了,建议,以后写代码的时候直接将该句加上**)

    ```
    <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: https://ssl.gatatic.com 'unsafe-eval'" >
    ```

  - ,其次,引入cordova.js文件

  - 最后,运行`npm run build`将文件打包成dist

## 3.Cordova

- 会将我们的js代码和css代码转化成安卓代码,以便打包出来的安卓的apk文件,但是它并不是完全转化,应用内的逻辑任然按照浏览器形式进行运行的
- 现在国内越来越多的开发者使用vue开发混合app,但是大家开发完毕之后不知道如何将其打包成app
- 目前vue最流行的就是weex和cordova,weex是由阿里提供并且由vue力荐的,但是用法比较难,不适合初学者学习

### 第一步:安装

```
cnpm install -g cordova
```

如果下一步创建cordova项目失败,那么尝试用cnpm去下载,因为新的cordova版本 如果用cnpm下载,会出现模块缺少的错误,所以建议大家用npm下载,如果npm无法下载,那么建议使用6.0.0版本进行发布

### 第二步:新建cordova项目

```
cordova create 项目名称
```

### 第三步:加入安卓依赖

进入cordova的项目文件夹 加入安卓依赖

```
cordova platform add android
```

