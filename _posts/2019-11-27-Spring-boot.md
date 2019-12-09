---
layout: post
title: Spring boot
date: 2019-11-27
categories: test
tags: Spring boot

---

# Spring boot

## 创建java项目

https://start.spring.io/

常用依赖包

- spring web
- MySql Driver
- MyBatis Framework
- Spring Boot DevTools
- Lombok

下载包就可以了

## @RestController

表示返回格式为json

@RestController是@controller与@ResponseBody组合

## Mapper

```java
//代表主键自增
@Options(useGeneratedKeys=true keyProperty="id")
```

## 数据验证@Valid

```java
public JsonResult create(@RequestBody @Valid CreateRequest request,BindingResult bindingResult){
	if(bindingResult.hasErrors()){
    return JsonResult(false,bindingResult.getFieldError().getDefaultMessage());
  }
}
```

## 开启事务

```java
//遇到异常自动回滚
@Transactional(rollbackFor = Exception.class)

//不会自动回滚
try{
    throw new RuntimeException();
}catch(RuntimeException e){
    e.printStackTrace();
}finally{
}

//会自动回滚
try{
    throw new RuntimeException();
}catch(RuntimeException e){
    e.printStackTrace();
    throw new RuntimeException();
}finally{
}
```

## dto与model之间的转换

```java
<dependency>
    <groupId>com.github.jmnarloch</groupId>
    <artifactId>modelmapper-spring-boot-starter</artifactId>
    <version>1.1.0</version>
</dependency>
```

## ModelMapper

开启严格模式 默认LOOSE 松散模式

```java
modelMapper.getConfiguration().setMatchingStrategy(MatchingStrategies.STRICT);
```

