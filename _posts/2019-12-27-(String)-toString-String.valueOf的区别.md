---
layout: post
title: (String) toString String.valueOf的区别
date: 2019-12-27
categories: test
tags: Java

---

## (String) toString String.valueOf的区别

**（String）**

强制类型转换，很常见的一种类型转换方式，使用这种方法时，需要注意的是类型必须能转成String类型。因此最好用instanceof做个类型检查，以判断是否可以转换。否则容易抛出CalssCastException异常。此外，需特别小心的是因定义为Object 类型的对象在转成String时语法检查并不会报错，这将可能导致潜在的错误存在。

备注：**null值可以强制转换为任何java类类型，(String)null是合法的**

 

**.toString()**

java.lang.Object类里已有public方法.toString()，而通常派生类会覆盖Object里的toString（）方法，所以对任何java对象都可以调用此方法。

必须**保证object不是null值**，否则将抛出NullPointerException异常



 **String.valueOf()**

此方法是String对象类型自带的转换方法，查看它的实现源码

```java
public static String valueOf(Object obj) {
    return (obj == null) ? "null" : obj.toString();
}
```

可以发现，它的实现是做了空判断之后再进行toString()，避免了NullPointerException空指针异常。

返回的是字符串null而不是null

