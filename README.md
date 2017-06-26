## 知乎爬虫

----------

## 需求

* php >= 7.0
* swoole 扩展

## 思路

首先是通过一个主文件传入操作类型，然后从配置文件里拿配置信息。

先拉取用户名，然后通过这个信息拉取用户详细信息。

#### 用户名获取

这是第一个表的内容

先在数据库写三五个种子用户名，然后通过数据库拿到这几个种子用户名，放入redis的链表结构中，

然后对redis的数据一个一个进行循环，每个用户名被拼接成`url`，随后curl就可以运行起来了。

获取到的页面信息传给分析器进行正则判断处理，随后发送回去。然后控制器把他们存入数据库。

当redis里的数据用完了就再从数据库拿数据。这时候数据库中就有上一轮存入的数据了。

如此循环，直到达到配置文件中要求。


## 问题

#### 性能问题

性能问题大大的。只是服务器不太好。不敢上多线程了。

#### 编码问题

我对于算法不算很懂，不过好歹知道一些性能问题，能在内存里运行的运算就放内存里了。

之前学了一些设计模式，用起来简直不要太爽！

## 解决方案

跑在了阿里云的学生机上，好棒

## Todo

* 解耦
* 日志
* 更好的错误处理

## Usage

1. 你首先需要拉取代码：
```bash
https://github.com/AnnatarHe/zhihuCrawler.git
```

2. 运行`Database`里面的数据库创建的一些东西

3. 运行index.php
```bash
php index.php&
```

4. 不出意外的话。。。速度较慢:flushed:

## 配置

在index.php里有一个常量定义：
```php
define(DEBUG, true);
```
真正跑数据的时候关掉，就好了

app\Config\里面有一些配置项，需要可以用
