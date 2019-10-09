---
layout: post
title: wordpress按层级方式显示分类链接的方法
date: 2019-10-08
categories: test
tags: wordpress
---

# wordpress按层级方式显示分类链接的方法

wordpress自带的模板有很都地方都比较难看，都不符合人性化设计，比如分类页面，只显示“分类归档：百度”这种样子，显然改成导航形式的比较好。

先看效果：

> [首页](http://www.51projob.com/) > [名企攻略](http://www.51projob.com/名企攻略) > [百度](http://www.51projob.com/名企攻略/百度)

这种样式的导航，首先让用户很清楚的知道自己所在的位置，其次对于搜索引擎来说也是很好的一个搜索优化。

#### 实现第一步：在模板目录下的functions.php中添加两个函数

```
function get_url_byLinkName($link, $name){
    return "<a href=\"$link\" title=\"$name\">$name</a>";
}

function get_hierarchy_category_path(){
    //来自疯狂的蚂蚁的博客www.crazyant.net
    //$wp_query是整个wordpress的全局变量，在任何地方都能够使用
    global $wp_query;
    //获取当前请求的参数中的分类ID
    $catid=$wp_query->query_vars['cat'];
    //获取首页的地址
    $home_url=get_url_byLinkName(home_url( '/' ),'首页');

    $result="";
    //采用迭代的方法获取上一级的分类信息
    while($catid!=0){
        $current_cat=get_category($catid);
        $current_cat_link = get_category_link( $catid );
        $current_cat_url=get_url_byLinkName(esc_url( $current_cat_link ),$current_cat->name);
        if($result){
            $result = "$current_cat_url > $result";    
        } else {
            $result = $current_cat_url;
        }
        //将父亲的分类ID付给迭代变量
        $catid=$current_cat->category_parent;
    }
    $result = "$home_url > $result";
    return $result;
}
```

 

第一个函数是为了偷懒，用其生成一个URL链接。第二个函数中，主要用到了wordpress的全局请求参数对象$wp_query还有分类的一些函数。

$wp_query对象请参考：http://codex.wordpress.org/Function_Reference/WP_Query

wordpress分类相关请参考：

- - - `is_category`
    - `in_category`
    - `cat_is_ancestor_of`
    - `get_category_parents`
    - `get_all_category_ids`
    - `get_categories`
    - `get_the_category`
    - `get_category`
    - `get_category_by_path`
    - `get_category_by_slug`
    - `get_cat_ID`
    - `get_cat_name`
    - `get_category_link`

在开发过程中，随时都可以使用print_r函数打印一下对象的内容，就知道怎样获取参数数据了。

#### 实现第二步：修改category.php模板文件替换导航

找到模板目录下的category.php文件，找到这个文字：

```
<h1 class="page-title">
<?php
printf( __( 'Category Archives: %s', 'twentyten' ), '<span>' . single_cat_title( '', false ) . '</span>' );
?>
</h1>
```

 

然后替换成调用我们编写的函数：

```
<h1 class="page-title">
<?php
echo get_hierarchy_category_path();
?>
</h1>
```

 

#### 总结

第一次开发wordpress函数（相当于小插件），整个过程一直在学习，官方的函数参考文档提供了几乎所有自己想要的函数和类：

[http://codex.wordpress.org/zh-cn:%E5%87%BD%E6%95%B0%E5%8F%82%E8%80%83](http://codex.wordpress.org/zh-cn:函数参考)

用的最多的应该就是全局变量$wp_query，当客户端请求服务器时，除了初始化配置，wordpress做的第一件事就是用HTTP请求参数初始化该全局变量，这样在代码的任何地方都可以随时引用。

比如本文的category.php中并没有给函数传递参数，因为在get_hierarchy_category_path中我们可以使用$wp_query这个全局变量获取所需的所有信息。