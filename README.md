
```
                                      ____    __    __    ____  _  _ 
                                     (  _ \  /__\  (  )  ( ___)( )/ )
                                      )(_) )/(__)\  )(__  )__)  )  ( 
                                     (____/(__)(__)(____)(____)(_)\_)
```
## 搭建
`chmod 777 -c build.sh`
`./build.sh`


## 测试
测试机器处理器：`i5-9300` ，系统 `Ubuntu 20.0.4`
```
webbench -c 10000 -t 4 http://localhost:1989/
```
结果：
```
Webbench - Simple Web Benchmark 1.5
Copyright (c) Radim Kolar 1997-2004, GPL Open Source Software.

Benchmarking: GET http://localhost:1989/
10000 clients, running 4 sec.

Speed=4841789 pages/min, 18630496 bytes/sec.
Requests: 322786 susceed, 0 failed.

```
## Dalek架构
`Master/Worker`模型，端口复用，使用时间轮管理长连接 ，每个工作进程创建一个`EventLoop`和`HttpServer`，`HttpServer`负责接受连接，注册连接进入`EventLoop`和`TimerWheel`。

## Dalek细节
`httppar.h`实现了一个高性能的http解析器，可以在客户端40ms发送1byte的情况下正确的解析http请求包 ，`reactor`目录下则对事件进行了抽象，任何IO事件都封装成`Channel`，包括定时事件`TimerWheel`，服务器事件`HttpServer`，连接事件`HttpConnection`


## 代码统计

| language | files | code | comment | blank | total | comment rate |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| C++ | 26 | 3,337 | 305 | 950 | 4,592 | 8.37% |
| Markdown | 4 | 36 | 0 | 10 | 46 | 0.00% |
| Makefile | 3 | 10 | 0 | 2 | 12 | 0.00% |
| Log | 1 | 5 | 0 | 1 | 6 | 0.00% |
| Shell Script | 1 | 3 | 1 | 1 | 5 | 25.00% |
## 代码树

```
Dalek
├─ CMakeLists.txt
├─ Dalek.cc
├─ base
│  ├─ SyncLogger.h
│  ├─ copyable.h
│  ├─ noncopyable.h
│  └─ swap.h
├─ build
├─ build.sh
├─ config.h
├─ http
│  ├─ Buffer.h
│  ├─ Dalek.cc
│  ├─ base.h
│  ├─ httpd.h
│  ├─ httppar.h
│  ├─ httpres.h
│  └─ mime.h
├─ json
│  └─ pson.h
└─ reactor
   ├─ Channel.h
   ├─ EventLoop.h
   ├─ InetAddress.h
   ├─ Poller.h
   ├─ Socket.h
   ├─ TimerWheel.h
   └─ base.h

```
## 参考
nginx
muduo
## TODO 
* Json 配置服务器
* 支持更多方法



```
Dalek
├─ CMakeLists.txt
├─ Dalek.cc
├─ README.md
├─ base
│  ├─ SyncLogger.h
│  ├─ copyable.h
│  ├─ noncopyable.h
│  └─ swap.h
├─ build
├─ build.sh
├─ http
│  ├─ Buffer.h
│  ├─ base.h
│  ├─ httpd.h
│  ├─ httppar.h
│  ├─ httpres.h
│  └─ mime.h
└─ reactor
   ├─ Channel.h
   ├─ EventLoop.h
   ├─ InetAddress.h
   ├─ Poller.h
   ├─ Socket.h
   ├─ TimerWheel.h
   └─ base.h

```