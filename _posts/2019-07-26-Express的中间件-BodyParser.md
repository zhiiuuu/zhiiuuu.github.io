---
layout: post
title: Express的中间件 BodyParser
date: 2019-07-26
categories: test
tags: Express
---

## Express的中间件 BodyParser

前端发送的数据请求需要后端获取，express的中间件模块body-parser可用于获取前端Post提交的数据

在app.js中加载该模块，并进行配置，body-parser提供了bodyParser.json(),bodyParser.raw(),bodyParser.text(),bodyParser.urlencode()四种解析数据的方法，其中最后一种支持utf-8的解析方式，bodyParser.urlencode()提供了多个参数，这里用到的是extended - 当设置为false时，会使用querystring库解析URL编码的数据；当设置为true时，会使用qs库解析URL编码的数据。后没有指定编码时，使用此编码。默认为true。

加载body-parser后，使用req.body即可获取前端传过来的post信息。

在http请求种，POST、PUT、PATCH三种请求方法中包含着请求体，也就是所谓的request，在Nodejs原生的http模块中，请求体是要基于流的方式来接受和解析。
 body-parser是一个HTTP请求体解析的中间件，使用这个模块可以解析JSON、Raw、文本、URL-encoded格式的请求体，

------

Node原生的http模块中，是将用户请求数据封装到了用于请求的对象req中，这个对象是一个IncomingMessage，该对象同时也是一个可读流对象。在原生Http服务器，或不依赖第三方解析模块时，可以用下面的方法请求并且解析请求体

```
    const http = require('http');

    http.createServer(function(req, res){
        if(req.method.toLowerCase() === 'post'){
            let body = '';
            //此步骤为接收数据
            req.on('data', function(chunk){
                body += chunk;
            });
            //开始解析
            req.on('end', function(){
                if(req.headers['content-type'].indexOf('application/json')!==-1){
                    JSON.parse(body);
                }else if(req.headers['content-type'].indexOf('application/octet-stream')!==-1){
                    //Rwa格式请求体解析
                }else if(req.headers['content-type'].indexOf('text/plain')!==-1){
                    //text文本格式请求体解析
                }else if(req.headers['content-type'].indexOf('application/x-www-form-urlencoded')!==-1){
                    //url-encoded格式请求体解析
                }else{
                //其他格式解析
                }
            })
        }else{
            res.end('其他方式提交')
        }
    }).listen(3000)
```

------

sudo wget http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz这样就可以在项目的application级别，引入了body-parser模块处理请求体。在上述代码中，模块会处理application/x-www-form-urlencoded、application/json两种格式的请求体。经过这个中间件后，就可以在所有路由处理器的req.body中访问请求参数

在实际项目中，不同路径可能要求用户使用不同的内容类型，body-parser还支持为单个express路由添加请求体解析，比如

```
var express = require('express');
var bodyParser = require('body-parser');

var app = new express();

//创建application/json解析
var jsonParser = bodyParser.json();

//创建application/x-www-form-urlencoded
var urlencodedParser = bodyParser.urlencoded({extended: false});

//POST /login 中获取URL编码的请求体
app.post('/login', urlencodedParser, function(req, res){
    if(!req.body) return res.sendStatus(400);
    res.send('welcome, ' + req.body.username);
})

//POST /api/users 获取JSON编码的请求体
app.post('/api/users', jsonParser, function(req,res){
    if(!req.body) return res.sendStatus(400);
    //create user in req.body
})
```

------

<<指定请求类型>>
 body-parser还支持为某一种或者某一类内容类型的请求体指定解析方式，指定时可以通过在解析方法中添加type参数修改指定Content-Type的解析方式。
 比如，对text/plain内容类型使用JSON解析

```
app.use(bodyParser.json({type: 'text/plain'}))
```

这一选项更多是用在非标准请求头中的解析

```
// 解析自定义的 JSON
app.use(bodyParser.json({ type: 'application/*+json' }))

// 解析自定义的 Buffer
app.use(bodyParser.raw({ type: 'application/vnd.custom-type' }))

// 将 HTML 请求体做为字符串处理
app.use(bodyParser.text({ type: 'text/html' }))
```

------

<<body-parser模块的API>>
 当请求体解析之后，解析值会被放到req.body属性中，当内容为空时候，为一个空对象{}
 ---bodyParser.json()--解析JSON格式
 ---bodyParser.raw()--解析二进制格式
 ---bodyParser.text()--解析文本格式
 ---bodyParser.urlencoded()--解析文本格式