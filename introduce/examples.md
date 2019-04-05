# 示例

## 项目示例

### Realworld backend server

[RealWorld.io](https://github.com/gothinkster/realworld) 是一个使用基于 Moleculer 微服务框架作为后端服务的示例。

#### 主要特征

- 7个微服务
- NeDB 或 MongoDB 数据库
- 用户登录和注册
- JWT 用户授权
- 内存缓存
- Docker

#### 源码

[https://github.com/moleculerjs/moleculer-examples/tree/master/conduit#readme](https://github.com/moleculerjs/moleculer-examples/tree/master/conduit#readme)

### Blog

一个简单的博客示例

#### 主要特征

- Docker files
- ExpressJS www server with Pug
- MongoDB database with moleculer-db and moleculer-db-adapter-mongoose modules
- NATS transporter
- Redis cacher
- Traefik reverse proxy (in micro arch)
- static frontend

#### 源码

[https://github.com/moleculerjs/moleculer-examples/blob/master/blog#readme](https://github.com/moleculerjs/moleculer-examples/blob/master/blog#readme)

### Short examples

Moleculer 中的一些示例

#### 简单示例

一个简单的 demo 示例，只有一个 math servie，支持两个数的加减乘除运算。

```shell
$ npm run demo simple
```

[Github 源码地址](https://github.com/moleculerjs/moleculer/blob/master/examples/simple/index.js)

#### 服务端 & 客户端

本例中，你可以启动任何一个服务端，客户端。服务端支持 math.add 方法。客户端会循环掉调用这个方法，并且可以对服务的或者客户端启动多个实例。本例中默认使用对 TCP 传输，你也可以通过环境变量 TRANSPORTER 配置成你想用的其他传输方式。

##### 启动服务端

```shell
$ node examples/client-server/server
```

##### 启动客户端

```shell
$ node examples/client-server/client
```

[Github 源码地址](https://github.com/moleculerjs/moleculer/tree/master/examples/client-server)

#### 中间件

中间件工作原理示例

```shell
$ npm run demo middlewares
```

[Github 源码地址](https://github.com/moleculerjs/moleculer/blob/master/examples/middlewares/index.js)

#### 运行

通过 [Moleculer Runner](https://moleculer.services/docs/0.13/moleculer-runner.html) 启动 broker 和加载 service 的示例

```shell
$ node ./bin/moleculer-runner.js -c examples/runner/moleculer.config.js -r examples/user.service.js
```

首先会通过配置文件 `moleculer.config.js` 中的配置参数来启动 broker，然后通过 `user.service.js` 文件加载 user service，并且将其转换成 REPL 模式。

[Github 源码地址](https://github.com/moleculerjs/moleculer/blob/master/examples/runner)

#### 负载测试仪

本例展示来如何启动一个负载测试，启动后，服务端和客户端会打印出每秒的请求数

##### 启动服务

```shell
$ node examples/loadtest/server
```

##### Start & fork clients (CPU核心数)

```shell
$ node examples/loadtest/clients
```

[Github 源码地址](https://github.com/moleculerjs/moleculer/blob/master/examples/loadtest)
