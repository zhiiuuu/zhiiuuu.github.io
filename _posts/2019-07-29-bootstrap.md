---
layout: post
title: bootstrap
date: 2019-07-29
categories: test
tags: bootstrap

---

# bootstrap

|          class           |                描述                |
| :----------------------: | :--------------------------------: |
|      img-responsive      |             响应式图像             |
|           lead           |      更大更粗/行高更高的文本       |
|       text-center        |              文本居中              |
|        pull-right        |               右浮动               |
|       list-inline        |        把所有列表放在同一行        |
|      dl-horizontal       |           dt dd在同一行            |
|       text-justify       |   段落中超出屏幕部分文字自动换行   |
| text-lowercase/uppercase |           设定文本大小写           |
|        form-group        |            获取最佳间距            |
|         sr-only          |       可以隐藏内联表单的标签       |
|     form-horizontal      |              水平表单              |
|   form-control-static    | 水平表单内的表单标签后放置纯文本时 |
|       img-rounded        |            图片圆角6px             |
|        img-circle        |            图片变成圆形            |
|      img-thumbnail       |   添加一些内边距和一个灰色的边框   |



#### HTML5文档类型

bootstrap使用到的某些HTML元素和CSS属性需要将页面设置为HTML5文档类型

#### 移动设备优先

相对于bootstrap2中,bootstrap3中,我们重写了整个框架,把针对移动设备的样式,直接融进了框架的内核中,也就是说,bootstrap是移动设备优先的

为了确保适当的绘制和触屏缩放,需要在`<head>`之中添加viewport元数据标签

```
<meta name="viewport" content="width=device-width,inital-scale=1">
```

排版与链接

boostrap排版、链接样式设置了基本的全局样式。分别是：

- 为`body`元素设置`background-color：#fff；`
- 使用`@font-family-base`、`@font-size-base`和`line-height-base`变量作为排版的基本参数
- 为所有链接设置了基本颜色`@link-color`，并且当链接处于`：hover`状态时添加下划线

这些样式都能在`scaffolding.less`文件中找到对应的源码

#### Normalize.css

为了增强跨浏览器表现的一致性，我们使用了normalize.css，这是由Nicolas Gallagher 和 Jonathan Neal维护的一个CSS重置样式库

Normalize。css是一个小的css文件，它在HTML元素的默认样式中提供了更好的跨浏览器一致性。它是一种现代的HTML5，可代替传统的CSS重置。

- 与许多CSS重置不同，保留有用的默认值
- 规范化各种元素的样式
- 更正了错误和常见的浏览器不一致性
- 通过微妙的修改提高可用性
- 使用详细注释说明代码的作用

#### 珊格参数

槽宽：30px









