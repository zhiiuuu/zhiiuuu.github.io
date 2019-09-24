---
layout: post
title: Laravel - Redis 缓存篇
date: 2019-09-06
categories: test
tags: Laravel Redis

---

# Laravel - Redis 缓存篇

## 一.基础篇

> Redis的使用场景想必大家多多少少都了解一些了。比如新浪的首页那么多模块，那么多文章，如果读数据库是不是压力特别大，反应是不是特别慢？但是为什么新浪为什么能很快的响应页面？其中一部分功劳就是靠的Reids的缓存技术。相比较Memcached笔者还是更喜欢Redis一点。

下面简单的分析一下，欢迎拍砖！

- Redis不仅仅支持简单的k/v类型的数据，同时还提供list，set，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。
- Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用。

Laravel中 使用的Redis

Redis 是一款开源且先进的键值对数据库。由于它可用的键包含了字符串、哈希、列表、集合 和 有序集合，因此常被称作数据结构服务器。在使用 Redis 之前，你必须通过 Composer 安装 predis/predis 扩展包（~1.0）。

## 1.laravel安装predis组件!!!

> composer require predis/predis

配置 应用程序的 Redis 设置都在 config/database.php 配置文件中。在这个文件里，你可以看到 redis 数组里面包含了应用程序使用的 Redis 服务器：



```
'redis' => [
    'cluster' => false,
    'default' => [
        'host'     => '127.0.0.1',
        'port'     => 6379,
        'database' => 0,
    ],
],
```

默认的服务器配置对于开发来说应该足够了。然而，你也可以根据使用的环境来随意更改数组。只需给每个 Redis 指定名称以及在服务器中使用的 host 和 port 即可。

## 2.服务器环境中安装redis

如果的环境配置中没有redis,请根据你的系统下载redis

## 3.小提示

```
如果你在下面的代码中不想写\Redis
可以use Redis
```

## 4.注意!注意!注意!

**运行代码时 请确保你环境中的redis服务是开启的**

**运行代码时 请确保你环境中的redis服务是开启的**

**运行代码时 请确保你环境中的redis服务是开启的**

windows

`redis-server.exe redis.windows.conf`





基本使用方法

------

STRING类型 - 写入字符串类型的redis



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'STRING:TEST';
        $value = 'Hello-World';
        // 写入一个字符串类型的redis
        $info = \Redis::Set($key,$value);
        dd($info);
        return view('test');
    }
}
```

- 读取相应的字符串



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'STRING:TEST';
        // 读取一个字符串类型的redis
        $info = \Redis::get($key);
        dd($info);
        return view('test');
    }
}
```

和redis语法同样的 字串也有incr和decr等递增、递减...

------

LIST类型

- 写入队列



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'LIST:TEST:R';
        $names = ['PHP','HTML','CSS','JavaScript','Node','Java','Ruby','Python'];
        // 从右往左压入队列
        $info = \Redis::rpush($key,$names);
        dd($info);
        return view('test');
    }
}
```

- 写入队列



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'LIST:TEST:R';
        $names = ['PHP','HTML','CSS','JavaScript','Node','Java','Ruby','Python'];
        // 获取队列内容(0到-1 所有 0到0是一位 0到1是两位)
        $info = \Redis::lrange($key,0,-1);
        dd($info);
        return view('test');
    }
}
```

- 从左往右塞入队列 连贯方法



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'LIST:TEST:L';
        $names = ['PHP','HTML','CSS','JavaScript','Node','Java','Ruby','Python'];
        // 从左往右存数据
        \Redis::lpush($key,$names);
        // 取出数据
        $info = \Redis::lrange($key,0,-1);
        dd($info);
        return view('test');
    }
}
```

HASH类型

- 存数据



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'HASH:TEST';
        $names = ['id'=>'99',
                  'name'=>'AXiBa',
                  'age'=>'23',
                  'tel'=>'13995578699',
                  'addtime'=>'1231231233'];
        // 将数据写入hash
        $info = \Redis::hMset($key,$names);
        dd($info);
        return view('test');
    }
}
```

- 取数据(取所有)



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'HASH:TEST';
        $names = ['id'=>'99',
                  'name'=>'AXiBa',
                  'age'=>'23',
                  'tel'=>'13995578699',
                  'addtime'=>'1231231233'];
        // 取出hash里的数据
        $info = \Redis::hGetall($key);
        dd($info);
        return view('test');
    }
}
```

- 取数据(取个别字段)



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'HASH:TEST';
        $names = ['id'=>'99',
                  'name'=>'AXiBa',
                  'age'=>'23',
                  'tel'=>'13995578699',
                  'addtime'=>'1231231233'];
        // 取出hash里的 某一个字段的数据
        $info = \Redis::hGet($key,'name');
        dd($info);
        return view('test');
    }
}
```



```
// 判断这个redis key是否存在
\Redis::exists($key)；
```

SET类型

- 写入一个无序集合(数据插入无顺序)



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'SET:TEST';
        $value = ['a','b','c','d','e'];
        $info = \Redis::sadd($key,$value);
         $info = \Redis::smembers($key);
        dd($info);
        return view('test');
    }
}
```

- 求两个集合的交集



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'SET:TEST';
        $key1 = 'SET:TEST:1';
        $value = ['a','b','c','d','e'];
        $value1 = ['a','b','c','1','2'];
        // 写入另一个集合
        \Redis::sadd($key1,$value1);
        // 交集
        $info = \Redis::sinter($key,$key1);
        dd($info);
        return view('test');
    }
}
```

- 求两个集合的并集

  ```
  class PhotoController extends Controller  
  {
      /**
       * Display a listing of the resource.
       *
       * @return \Illuminate\Http\Response
       */
      public function index()
      {
          //
          $key = 'SET:TEST';
          $key1 = 'SET:TEST:1';
          $value = ['a','b','c','d','e'];
          $value1 = ['a','b','c','1','2'];
          // 并集
          $info = \Redis::sunion($key,$key1);
          dd($info);
          return view('test');
      }
  }
  ```


- 求两个集合的差集



```
class PhotoController extends Controller  
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $key = 'SET:TEST';
        $key1 = 'SET:TEST:1';
        $value = ['a','b','c','d','e'];
        $value1 = ['a','b','c','1','2'];
        // 差集
        $info = \Redis::sdiff($key,$key1);
        dd($info);
        return view('test');
    }
}
```

哪个key在前，就以哪个key的值为基准。。



## 二.Predis -基本数据隔离

队列如何配合STRING类型或者HASH类型来组合使用，甚至把非关系变成和MySQl一样成为关系型的。



### 队列与哈希的组合使用 - 实现数据关系化

> 思路 :利用队列里的值来做需要取数据的唯一索引，利用哈希的key的后缀名做原型数据的唯一索引

队列和哈希的组合使用优势是，取出来可以直接使用，劣势在于内存占用相比较字符串而言要大

- 实例:因为Redis只能存数组而我们实例为了方便直接用DB类来写的，如果是ORM可以直接返回数组的



```
/**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $where = ['status'=>'1'];
        $obj = \DB::table('data_admin_login')->where($where)->get();
        $array = $this->objectToArray($obj);
        dd($array);
    }
```

- 接下来 我们要把从数据库取出来的数据存入Redis，用什么样的方法存，用什么样的方法取，这些东西都得考虑好；下面实例如下：



```
	/**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $where = ['status'=>'1'];
        $obj = \DB::table('data_admin_login')->where($where)->get();
        $array = $this->objectToArray($obj);
        // 定义Redis的key
        $listKey = 'LIST:TEST:ADMIN';
        $hashKey = 'HASH:TEST:ADMIN:';
        // 遍历时写入Redis list为索引 hash为数据
        foreach($array as $v){
            \Redis::rpush($listKey,$v['guid']);
            \Redis::hMset($hashKey.$v['guid'],$v);
        }
        return '缓存写入成功';
    }
```

- 查看下redis里面的情况 第一个 查看所有key 发现有1个队列和16个哈希
  第二个 取LIST:TEST:ADMIN 整个队列 发现有16个 唯一识别ID的数据（而且顺序和从数据库取出来的顺序是一样的）

第三个取出其中一个哈希查看数据

- 可以看出来 我们想要的数据已经存入了redis中，接下来，如果我想通过redis直接获取MySQL中管理员的列表数据怎么使用呢?



```
/**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        // 定义Redis的key
        $listKey = 'LIST:TEST:ADMIN';
        $hashKey = 'HASH:TEST:ADMIN:';
        // 取出admin队列的唯一识别id数组
        $list = \Redis::lrange($listKey,0,-1);
        $array = null;
        foreach($list as $v){
            // 取出哈希里的数据写入大数组中
            $array[] = \Redis::hGetall($hashKey.$v);
        }
        dd($array);
    }
```

这样取出来的数据是不是一样可以遍历到模版上？

- 最后来完整的做一个例子

  > 思路：我们的目的是从redis里面取出想要输出到模版上的数据，但是redis大家也知道，只是缓存服务器重启了，就没了（除非做磁盘持久化）,但是我要做的是如果Redis里面没有我要从MySQL里面取，取到了然后写入Redis，保证对MySQL的请求大大减少。



```
/**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        // 定义Redis的key
        $listKey = 'LIST:TEST:ADMIN';
        $hashKey = 'HASH:TEST:ADMIN:';
        // 查看key是否存在？
        if(empty(\Redis::exists($listKey))){
            // 如果Redis不存在 读数据库然后写入redis
            $where = ['status'=>'1'];
            $obj = \DB::table('data_admin_login')->where($where)->get();
            $array = $this->objectToArray($obj);
            // 遍历时写入Redis list为索引 hash为数据
            foreach($array as $v){
                \Redis::rpush($listKey,$v['guid']);
                \Redis::hMset($hashKey.$v['guid'],$v);
            }
            return $array;
        }
        // 如果redis存在 直接读redis的数据
        // 取出admin队列的唯一识别id数组
        $list = \Redis::lrange($listKey,0,-1);
        $array = null;
        foreach($list as $v){
            $array[] = \Redis::hGetall($hashKey.$v);
        }
        return $array;
    }
```
    * 不管我把redis的key手动删除还是redis的key存在 我们输出的都是这个(这是我的浏览器插件json-handle的效果)
    * 删除redis的key 效果依旧
那么肯定有人又要问了 你这只是在读数据库 如果我增 删 改 后 redis不同步了哇
是这样的，所以一般我们在实际商业项目中 做一个大型的redis数据隔离都需要把mysql的增删改 绑上同步的redis操作，这样下来，我每次读redis既大大的提升了性能，也保障了数据的同步性
下面拿添加做一个实例，如何MySQL与redis数据同步
restfulApi 添加方法
```

- redis查看一下有没有同步写入
  我们发现数据同步进入了redis
- index方法代码不变 再请求一次 数据也明显同步了

> 以上讲的就是最基本的redis隔离技术，当然为了提现的简单点，直接都写在控制器里面了，并没有做过多的分层调用，RedisKey也没有做配置话，而是反复在用；实际项目中Redis是可以单独做一个模块的，架构的层级分化明确了也可以大大的提升Redis的复用性;当然这些只是建议和思路，主要还是看当前每个人手头的架构为主。

其他组合关系型方法

至于其他的关系型的组合方法就在下面简要做做介绍了,纯手码写得也挺累，望大家体谅。。

- 队列和字符串类型
  队列和字符串类型一样可以把数据关系型

> 思路：同样的list存索引的key(ID或唯一识别ID),字符串存json字符串,字符串的key同样后缀加唯一识别ID来进行区分。当需要输出到页面上的时候json_decode过来就行了

队列和字符串的优点是存储的空间小，劣势在于存的时候要解析成字符串，取的时候要解析为数组或对象

- 集合和字符串类型
  集合和字符串类型一样可以把数据关系型

> 思路：大家应该都知道 redis集合有有序集合和无序集合之分，在有些场景中，其实用集合的形式反而更灵活（多维度集合控制），比如 关注我的人、我关注的人、同时互相关注的、QQ中的'可能认识的人'、异步写入时分区间等等等...

- 集合和哈希类型
  思路其实就是和上面差不多，也就是存储方便，消耗内存相比较而言较大。

> 参考 redis中文官网 <http://www.redis.cn/>
> 参考 易百教程 <http://www.yiibai.com/redis/redis_environment.html>
```