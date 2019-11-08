---
layout: post
title: Docker Nginx Node.js
date: 2019-11-08
categories: test
tags: docker

---

# Docker Nginx Node.js

> 部署之前 请先学习docker的基本命令

docker基本知识 [点击这里](https://github.com/zhiiuuu/docker-notes "With a Title")

docker-lnmp  [点击这里](https://github.com/zhiiuuu/docker-lnmp "With a Title")

docker-node.js [docker命令](https://hub.docker.com/_/node/ "with a title") [nodejs镜像的使用](https://github.com/nodejs/docker-node/blob/master/README.md#how-to-use-this-image "with a title")

### windows下创建数据卷

大部分的盘符式 是不能用的 应该使用命令 挂载

```
//比如你的本机数据是在
E:\docker1\vue_ant_product_admin

//你挂载的时候就应该这样
-v /e/docker1/vue_ant_product_admin:/usr/src/app/
```

