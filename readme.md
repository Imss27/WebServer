# WebServer
A webserver implemented by using C++.

## Funtions
* 利用IO复用技术Epoll与线程池实现多线程的Reactor高并发模型；
* 利用正则与状态机解析HTTP请求报文，实现处理静态资源的请求；
* 利用标准库容器封装char，实现自动增长的缓冲区；
* 基于小根堆实现的定时器，关闭超时的非活动连接；
* 利用单例模式与阻塞队列实现异步的日志系统，记录服务器运行状态；
* 利用RAII机制实现了数据库连接池，减少数据库连接建立与关闭的开销，同时实现了用户注册登录功能。

* 增加logsys,threadpool测试单元(todo: timer, sqlconnpool, httprequest, httpresponse) 

## Requirements
* Linux
* C++14
* MySql

## Directory Tree
```
.
├── code           //source code
│   ├── buffer
│   ├── config
│   ├── http
│   ├── log
│   ├── timer
│   ├── pool
│   ├── server
│   └── main.cpp
├── test           //unit test
│   ├── Makefile
│   └── test.cpp
├── resources      //web
│   ├── index.html
│   ├── image
│   ├── video
│   ├── js
│   └── css
├── bin            //executable
│   └── server
├── log            
├── webbench-1.5   //performance test
├── build          
│   └── Makefile
├── Makefile
├── LICENSE
└── readme.md
```


## Init
需要先配置好对应的数据库
```bash
// 建立yourdb库
create database yourdb;

// 创建user表
USE yourdb;
CREATE TABLE user(
    username char(50) NULL,
    password char(50) NULL
)ENGINE=InnoDB;

// 添加数据
INSERT INTO user(username, password) VALUES('name', 'password');
```

```bash
make
./bin/server
```

## Unit test
```bash
cd test
make
./test
```

## Performance Test
![image-webbench](https://github.com/markparticle/WebServer/blob/master/readme.assest/%E5%8E%8B%E5%8A%9B%E6%B5%8B%E8%AF%95.png)
```bash
./webbench-1.5/webbench -c 100 -t 10 http://ip:port/
./webbench-1.5/webbench -c 1000 -t 10 http://ip:port/
./webbench-1.5/webbench -c 5000 -t 10 http://ip:port/
./webbench-1.5/webbench -c 10000 -t 10 http://ip:port/
```
* 测试环境: Ubuntu:20.04 cpu:i5-8400 内存:8G 
* QPS 4000+

## TODO


## Acknowlegdement
《Linux高性能服务器编程》，游双.

[@qinguoyi](https://github.com/qinguoyi/TinyWebServer)
