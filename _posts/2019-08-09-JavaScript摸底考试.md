---
layout: post
title: JavaScript摸底考试
date: 2019-08-09
categories: test
tags: JavaScript
---

# JavaScript摸底考试

> 出题: 邹义良 2019-08-08

## 不定项选择题，0个或多个，如果没有正确答案，填E

1. 以下说法正确的是(abcd)

   ```none
   A. js是跨平台、面向对象的动态编程语言
   B. js是一种具有函数优先的解释型编程语言 var 变量名 = function(){}
   C. js是基于原型、多范式的编程语言 原型链的继承是什么 函数式编程 面向过程的编程
   D. js的核心语言叫ECMAScript ECMA组织中文名
   ```

2. 以下说法正确的是(abcd)

   ```none
   A. js能运行在浏览器中
   B. js能运行在服务端
   C. js能绘制出动态图像
   D. js具有基于事件循环的并发模型
   ```

3. 下面代码运行结果(c)

   ```none
   var userName = "jack"
   console.log(username)
   
   A. 输出:jack
   B. 报错:缺少分号
   C. 报错: username is not defined
   D. 报错: console.log is not a function
   ```

4. 下面代码运行结果(A)

   ```none
   if(true){
       var foo = 1
       let bar = 2
   }
   
   console.log(foo)
   console.log(bar)
   
   A. 输出 1 然后报错 bar is not defined
   B. 输出 1 2
   C. 报错 foo is not defined 然后输出 2
   D. 没有输出，只报错 bar is not defined
   ```

5. 下面代码运行结果(C)

   ```none
   var a = 1
   var a = 2
   {
       let a = 3
   }
   console.log(a)
   
   A. Identifier 'a' has already been declared
   B. Uncaught SyntaxError: Unexpected identifier
   C. 输出2
   D. 输出3
   
   //let是在花括号里的 且不能let两次
   ```

6. 下面代码运行结果(A)

   ```none
   const PI = 3.14
   function test(){
       var PI = 3.14159
   }
   test()
   console.log(PI)
   
   A. 输出 3.14
   B. 输出 3.14159
   C. Identifier 'PI' has already been declared
   ```

7. 下面代码运行结果(D)

   ```none
   let foo = 1
   const bar = 2
   foo = 3
   bar = 4
   console.log(foo)
   console.log(bar)
   
   A. 输出 3 4
   B. 输出 3 2
   C. 输出 1 2
   D. 报错 Assignment to constant variable
   ```

8. 下面代码能正确运行的有(AB)

   ```none
   A. var 姓名 = "张三";       console.log(姓名)
   B. var $name = "李四";     console.log($name)
   C. var 7niu = "王五";      console.log(7niu)
   D. var user-name = "赵六"; console.log(user-name)
   
   MYSQL	UTF8不能存用户的表情 
   ```

9. 下面代码运行结果(B)

   ```none
   var foo
   console.log(foo)
   
   A. null
   B. undefined
   C. false
   D. None
   ```

10. 下面代码运行结果(A)

    ```none
    var myvar = "foo"
    
    function test(){
      console.log(myvar)
      var myvar = "bar"
    }
    test()
    
    A. undefined
    B. null
    C. foo
    D. bar
    ```

11. 下面代码在Chrome中运行结果(C)

    ```none
    var myvar = "foo";
    
    console.log(myvar)
    console.log(window.myvar)
    console.log(globalThis.myvar)
    
    A. foo undefined undefined
    B. foo null null
    C. foo foo foo
    D. foo 
        window.myvar is not defined 
        globalThis.myvar is not defined 
        
        
    //console.log()不属于js
    //宿主
    //js global 在浏览器中 都是 globalThis
    //浏览器WINDOW代表顶层对象global
    ```

12. 最新的 ECMAScript 标准定义的数据类型，选出正确的(ABD)

    ```none
    A. boolean、number 3/0正无穷大
    B. null、undefined
    C. int、string
    D. symbol、object
    
    //bigint
    ```

13. 下面代码运行结果(D)

    ```none
    var a = 1
    var b = 2
    var c = "3"
    console.log(a+b+c)
    console.log(a+c-b)
    
    A. 6   2
    B. 123 2
    C. 15  11
    D. 33  11 
    ```

14. 下面代码运行结果(D)

    ```none
    var n = "2"
    switch(n){
        case 1:
            console.log("星期一")
        case 2:
            console.log("星期二")
    }
    
    A. 星期一
    B. 星期二
    C. 星期一 星期二
    D. 什么也不输出
    ```

15. 下面代码运行结果(A)

    ```none
    function test(n){
        try{
            throw new Error("foo")
            console.log(n)
        }catch(e){
            console.log(e.message)
            return
        }finally{
            console.log("{$n}")
        }
    }
    
    test("bar");
    
    A. foo {$n}
    B. foo bar
    C. bar foo
    D. bar foo {$n}
    
    JS解析变量反引号${变量名}
    ```

16. 下面代码运行结果(C)

    ```none
    for(var i=0;i<=3;i++){
        if(i==2){
            continue
        }
        console.log(i)
    }
    
    A. 0 1
    B. 0 1 2
    C. 0 1 3
    D. 0 2 3
    ```

17. 下面代码运行结果(A)

    ```none
    var data = ['a','b','c','d']
    for(var i in [1,2,3]){
        console.log(data[i])
    }
    
    A. abc
    B. bcd
    C. 123
    C. 012
    ```

18. 下面代码运行结果(D)

    ```none
    let arr = [3, 5, 7];
    arr.foo = "hello";
    
    for (let i of arr) {
       console.log(i)
    }
    
    A. 0 1 2 foo
    B. 3 5 7
    C. 0 1 2 hello
    D. 3 5 7 hello
    ```

19. 下面代码能正确输出3的是(B)

    ```none
    let arr = [3, 5, 7];
    A. console.log(arr.count)
    B. console.log(arr.length)
    C. console.log(len(arr))
    D. console.log(size(arr))
    ```

20. 下面代码运行结果(B)

    ```none
    var s = new Set()
    s.add(1)
    s.add(1)
    console.log(s.size)
    
    A. 0
    B. 1
    C. 2
    D. 报错
    ```

21. 下面代码运行结果(C)

    ```none
    var name = 'mary'
    var foo = {
        name:'jack',
        say1:function(){console.log(this.name)},
        say2(){console.log(this.name)},//===say:function(){}
        say3:()=>{console.log(this.name)},//箭头函数没有this
    }
    foo.say1()
    foo.say2()
    foo.say3()
    
    A. jack mary undefined
    B. jack jack jack
    C. jack jack mary
    D. jack jack undefined
    ```

22. 下面代码运行结果(A)

    ```none
    var a = "b"
    var user = {
        a,				//	"a":a;简写
        [a]:"c",	//[a] = 变量a
        "c":"d"
    }
    console.log(user.a)
    console.log(user.b)
    console.log(user.c)
    console.log(user[a])
    
    A. b c d c
    B. b undefined d b
    C. a undefined d undefined
    D. b c d undefined
    ```

23. 下面代码运行结果(D)

    ```none
    const p1 = new Promise(function (resolve, reject) {
        setTimeout(() => resolve("data1"), 2000)//resolve执行成功
    })
    
    const p2 = new Promise(function (resolve, reject) {
        setTimeout(() => reject(new Error('fail')), 1000)//reject执行失败
    })
    
    Promise.all([p1, p2]).then(result => {			
    //promise.all()会等两个函数 都返回 且都是成功的才会执行
        console.log(result[0])
        console.log(result[1])
    }).catch(error => console.log(error.message))
    //其中有一个失败了 所以执行catch 且只会执行一次catch
    
    A. data1 fail
    B. fail data1
    C. fail fail
    D. fail
    ```

24. 下面代码能正确将该div的类名改为active的是(B)

    ```none
    <div id="foo" class="invalid">
    
    A. document.getElementById('foo').class="active"
    B. document.getElementById('foo').className="active"
    C. document.getElementById('#foo').className="active"
    D. document.getElementById('#foo').class="active"
    ```

25. 下面代码运行结果(B)

    ```none
    var f = (function(i){
        console.log(i)
        i++
        return function(i){
            console.log(i)
        }
    })
    
    f(2)(3)
    
    A. 2 2
    B. 2 3
    C. 2 4
    D. 3 4
    ```