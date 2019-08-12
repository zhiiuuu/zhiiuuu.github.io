---
layout: post
title: 使用 VSCode 编辑器来编译 Sass
date: 2019-08-08
categories: test
tags: VSCode

---

# 使用 VSCode 编辑器来编译 Sass

**VSCode** 是继 Sublime Text3、Atom 后另一个让我爱不释手的编辑器，其颜值和插件生态圈与 Atom 不相上下，但比后者用起来更加丝滑流畅（Atom 需要4G+内存和SSD 才能逆天），所以自然成了我目前首选的编辑器。

------

前端项目自然少不了和 Sass 打交道，VSCode 提供了丰富的相关插件来帮助我们处理 Sass 相关任务。我用的是 Easy Sass 这款插件，目前最新版本是 0.0.6。

由于 Sass 的编译依赖 Ruby 环境，因此我们在开始之前**首先得安装 Ruby**，别担心，装 Ruby 只是为了提供运行环境，不懂 Ruby 没任何关系。[官网下载传送门](https://rubyinstaller.org/downloads/)

安装 Ruby 时一定要勾选 *Add Ruby executables to your PATH*，用来将 Ruby 添加到系统变量，这样后续可以省却很多不必要的麻烦。装好后在命令行输入 *gem sass* 来**安装 Sass**，安装完成后启动 VSCode，在拓展商店里**搜索“easy sass”，并安装**，安装成功后重启 VSCode。
![east](https://img.mukewang.com/597ee61e000181bc03610260.png)

接下来进行配置。在 VSCode 菜单栏依次点击“文件 首选项 设置”，打开 settings.json 全局配置文件。搜索“easysass”，然后把 easysass 相关的设置项复制到右侧的用户设置编辑窗口中，再根据实际情况修改配置项。
注意这里的配置项是全局的，不是只针对当前 VSCode 中打开的项目。换句话说，如果你在 VSCode 中切换了项目，应按实际情况再次调整 easysass 的配置项。

![settings](https://img.mukewang.com/597ee7890001731e07500418.png)

所有的默认配置项如下：

```
"easysass.compileAfterSave": true,

"easysass.excludeRegex": "",

"easysass.formats": [
    {
      "format": "expanded",
      "extension": ".css"
    },
    {
      "format": "compressed",
      "extension": ".min.css"
    }
],

"easysass.targetDir": ""
```

- `easysass.compileAfterSave` 保存 scss 或 sass 文件后自动进行编译。默认为 true。一般设为 true，可提高工作效率，如果项目中有不直接编译的文件，例如 variable.scss、theme.scss、mixin.scss 等，建议设为 false，避免这类文件编辑保存后被编译为无效 css 需要手动删除的尴尬。

- `easysass.excludeRegex` 提供一个文件名的正则表达式，匹配的文件会被排除，不会被编译成 css。默认为空，即该功能关闭。个人建议将一些不直接编译的文件以下划线开头命名，例如：*mixin.scss，然后设置：`"easysass.excludeRegex": "^*+"`，即可排除所有以下划线开头的 scss/sass 文件。

- `easysass.formats` 定义输出 css 文件的排版风格和文件名，是一个数组，可以同时编译输出多个不同风格、文件名的 css 文件。每个数组对象中有两个参数：

  1. `easysass.formats[i].format` 用以编译生成对应风格的 css，参数值如下：

     > *nested*：嵌套缩进的 css 代码。
     > *expanded*：没有缩进的、扩展的css代码。
     > *compact*：简洁格式的 css 代码。
     > *compressed*：压缩后的 css 代码。

  2. `easysass.formats[i].extension` 顾名思义就是设置编译输出的文件拓展名了，此处可以自定义文件名，输出的 css 文件名会按照“当前 Sass 文件名（不含拓展名）+此处自定义文件名”的格式来生成。
     例如：设置 `"easysass.formats[i].extension": ".min.css"`，假设当前的 Sass 文件名为
     *style.scss*，则编译输出的 css 文件名为 *style.min.css*。

- `easysass.targetDir` 我们在生产环境中很多情况下 scss/sass 文件和 css 文件是不在同一个目录下的，而 Easy Sass 默认输出的 css 是和当前 Sass 文件处于相同目录的，为此我们需要通过该参数来配置输出路径。
  参数值可以是绝对路径或相对路径。如果是相对路径，则以 VSCode 当前打开的项目的根目录为基准。
  ~~例如：设置 *easysass.targetDir* 为 "./css/"，此时保存修改完毕的 Sass 文件，VSCode 会自动编译并在当前 Sass 文件的上级文件夹 css 目录下输出生成 css 文件（见下图）。~~

例如下图的文件结构，项目根目录是 `TEST` 文件夹，scss 文件存放于 `sass` 文件夹，编译输出目录是 `css` 文件，则配置为：`"easysass.targetDir": "css/"`（"css" 后面的斜线也可省略）。

![生成css路径](https://img.mukewang.com/597ef078000131b403060211.png)

本文所述的只是采用 VSCode 编辑器编译生成 CSS 的一种方式，可能比较原始，实际生产环境中大多采用自动化构建方案，比如 grunt、gulp、fis 等。