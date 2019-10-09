---
layout: post
title: wordpress
date: 2019-10-08
categories: test
tags: wordpress

---

# wordpress

## 获取该文章的分类信息

1. $category = get_the_category();//默认获取当前所属分类
2. echo $category[0]->cat_ID; //输出分类 id

函数返回值：

- cat_ID - 分类 ID ，
- cat_name - 分类名 ，
- category_nicename - 别名 ，
- category_description - 分类描述 ，
- category_parent - 父分类 ID ，
- category_count - 包涵文章数量

## 根据分类id获取该分类下的文章

```
<?php $args = array(
                    'cat' => $cateid,
                    );
                    $query = new WP_Query( $args );
                    if ($query->have_posts()) : while ($query->have_posts()) : $query->the_post(); ?>
<?php endwhile;endif; ?>
```

```
get_posts("category=12")
```



## 制作文章页面single.php

**可以调用的文章内容：**

调用文章标题：<?php the_title(); ?>

调用文章内容：<?php the_content(); ?>

调用文章摘要：<?php the_excerpt(); ?>

调用作者姓名：<?php the_author(); ?>

调用文章发布时间：<?php the_time(); ?>

调用作者的Gravatar头像：<?php echo get_avatar( get_the_author_email(), 36 ); ?>

调用文章内容可以写：

```
<?php echo the_content();?>
```

但是这个wordpress会自动在段落上加上p，解决方法可以改为下面的写法

```
<?php 
$post=get_post(get_the_ID());
echo $post->post_content;
?>
```

 

post_author：(整数）文章作者的编号

post_date：(字符）文章发表的日期和时间（YYYY-MM-DD HH-MM-SS)

post_date_gmt：（字符）文章发表的格林尼治标准时间（GMT） （YYYY-MM-DD HH-MM-SS)

post_content：（字符）文章内容

post_title：（字符）文章标题

post_category：（整数）文章类别的编号。注意：该值在WordPress 2.1之后的版本总为0。定义文章的类别时可使用 get_the_category()函数。

post_excerpt：（字符）文章摘要

post_status：(字符）文章状态（publish|pending|draft|private|static|object|attachment|inherit|future）

comment_status：（字符）评论状态（open|closed|registered_only）

ping_status：（字符）pingback/trackback状态（open|closed）

post_password：(字符）文章密码

post_name：(字符）文章的URL嵌套

to_ping：(字符）要引用的URL链接

pinged：（字符）引用过的链接

post_modified：(字符）文章最后修改时间（YYYY-MM-DD HH-MM-SS)

post_modified_gmt：(字符）文章最后修改GMT时间（YYYY-MM-DD HH-MM-SS)

post_parent：(整数）父级文章编号（供附件等）

guid：（字符）文章的一个链接。注意：不能将GUID作为永久链接（虽然在2.5之前的版本中它的确被当作永久链接），也不能将它作为文章的可用链接。GUID是一种独有的标识符，只是目前恰巧成为文章的一个链接。

post_type：（字符）（日志 | 页面 | 附件）

 

 

常用：

```
发表于：<?php the_time('Y-h-d'); ?>
分类：<?php the_category(','); ?>
```

 引入评论框：

http://www.cnblogs.com/tinyphp/p/6366809.html

 

设置和获取浏览次数：

http://www.cnblogs.com/tinyphp/p/6366022.html





```
is_home() 是否是主页
is_single() 是否是文章详情页
is_admin() 是否是后台页
```

