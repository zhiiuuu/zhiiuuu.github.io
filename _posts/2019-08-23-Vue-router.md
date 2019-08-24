---
layout: post
title:  Vue-router
date: 2019-08-23
categories: test
tags: Vue

---

# Vue-router

### 1. **什么是路由？**

路由，其实就是指向的意思，当我们点击页面上的Home按钮的时候，页面就要显示Home的内容，如果点击页面上的about按钮，页面中就要显示about的内容

### 2. **路由中的三个概念**

(1) route，他是一条路由，是单数形式，比如Home按钮=>Home内容

(2) Routes，他是一组路由，是复数形式，或者说是一个数组。

[{Home按钮=>Home内容}，{about按钮=>about内容}]

(3) Router，是一个机制，相当于管理者，由他来管理路由。

### 3. **页面中的路由使用**

(1) 在HTML页面中

我们定义路由需要用到两个标签，第一个标签是<router-link>和<router-view>,他们分别表示页面中点击的部分和显示的部分。

(2) 在JS中配置路由

首先，第一步，必须要引入Vue以及Vue-Router模块，并且要调用一次use函数，并且把Router以参数的形式传入

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps3.jpg) 

然后需要配置路由，配置路由需要定义一个route或者routes，并且有两个属性，第一个属性是path，第二个属性是component。

Path指的是路径比如，规定www.abcd.com/about是关于页，那么/about就是我们所谓的路径。

Component指的是组件，比如，/about的时候需要展示about的内容，那么此时对应的component的值就是about。

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps4.jpg) 

(3) 最后需要对创建的路由进行管理

需要将定义好的routes传递给VueRouter对象

​    ![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps5.jpg)

(4) 重定向

如果首次进入页面，姐没有输入/home也没有输入/about，那么他的路径就是/那么此时需要重定向，如果有人直接进入页面，应该给他展示/home的内容。

如果输入没有定义的路径，那么让他直接进入首页。

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps6.jpg) 

 

### 4. **动态路由**

比如：当用户登录注册成功之后，会显示欢迎回来：XXX这时，XXX部分也就是用户的名字需要通过组件传递过来。

(1) 配置动态路由：直接在路由配置的路径后面加上id属性

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps7.jpg) 

(2) 接收动态路由的动态部分

需要用到一个方法，

```
this.$route.params.id
```

该方法需要添加到路由引入的组件

​    ![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps8.jpg)

### 5. **命名路由**

路由有一个名字，那么就直接给这个路由加一个name属性就可以了

如果user路由加了name属性

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps9.jpg) 

那么在app.vue中可以以以下形式进行路由跳转

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps10.jpg) 

### 6. **嵌套路由**

如果出现路由里面嵌套路由的情况，需要注意，在router-link中的to属性必须要写上一层路由

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps11.jpg) 

在配置路由的情况下，需要给父级路由添加children属性，配置子路由

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml9700\wps12.jpg) 





