---
layout: post
title: 卸载安装node npm (Mac linux )
date: 2019-07-26
categories: test
tags: uninstall

---

## 卸载安装node npm (Mac linux )

1. 卸载node npm

​      (1) 先卸载 npm:

```
sudo npm uninstall npm -g
```

　　(2) 然后卸载 Node.js.

　　(2.1) 如果是 Ubuntu 系统并使用 apt-get 安装的，可以使用命令：

```
sudo apt-get remove nodejs
```

　　(2.2)源文件安装的node, 卸载方式：首先cd到解压后到目录：　

```
sudo make uninstall
```

​     (2.3)mac 平台下brew安装的node（brew install node）, 卸载方式：

　　1.使用 **brew uninstall node** 命令卸载
　　2.在终端下执行命令，卸载node其他相关目录

```
　　sudo rm -rf /usr/local/{lib/node{,/.npm,_modules},bin,share/man}/{npm*,node*,man1/node*}
```

　　3.执行 **brew doctor** 命令，查看还有哪些与node、npm相关的目录，并删除。之前因为缺少这一步骤，导致一直未完全卸载。

#### 2. 安装node npm（Linux. Mac）

## Linux 上安装 Node.js

### 直接使用已编译好的包

Node 官网已经把 linux 下载版本更改为已编译好的版本了，我们可以直接下载解压后使用：

```
# wget https://nodejs.org/dist/v10.9.0/node-v10.9.0-linux-x64.tar.xz    // 下载
# tar xf  node-v10.9.0-linux-x64.tar.xz       // 解压
# cd node-v10.9.0-linux-x64/                  // 进入解压目录
# ./bin/node -v                               // 执行node命令 查看版本
v10.9.0
```

解压文件的 bin 目录底下包含了 node、npm 等命令，我们可以使用 ln 命令来设置软连接：

```
ln -s /usr/software/nodejs/bin/npm   /usr/local/bin/ 
ln -s /usr/software/nodejs/bin/node   /usr/local/bin/
```

### Ubuntu 源码安装 Node.js

以下部分我们将介绍在 Ubuntu Linux 下使用源码安装 Node.js 。 其他的 Linux 系统，如 Centos 等类似如下安装步骤。

在 Github 上获取 Node.js 源码：



```
$ sudo git clone https://github.com/nodejs/node.git
Cloning into 'node'...
```

修改目录权限：

```
$ sudo chmod -R 755 node
```

使用 **./configure** 创建编译文件，并按照：

```
$ cd node
$ sudo ./configure
$ sudo make
$ sudo make install
```

查看 node 版本：

```
$ node --version
v0.10.25
```

### Ubuntu apt-get命令安装

命令格式如下：

```
sudo apt-get install nodejs
sudo apt-get install npm
```