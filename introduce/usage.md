# 使用

## 安装 Moleculer

可以使用 npm 或 yarn 安装 moleculer

```shell
$ npm i moleculer --save
```

## 创建你的第一个微服务

下面我们将创建一个 math service，这个 service 有一个 add 方法可以计算两个数的和。

```javasript
const { ServiceBroker } = require("moleculer");

const broker = new ServiceBroker();

broker.createService({
    name: "math",
    actions: {
        add(ctx) {
            return Number(ctx.params.a) + Number(ctx.params.b);
        }
    }
});

broker.start()
    // Call service
    .then(() => broker.call("math.add", { a: 5, b: 3 }))
    .then(res => console.log("5 + 3 =", res))
    .catch(err => console.error(`Error occured! ${err.message}`));
```

> 在你的浏览器里访问试试！
>
> 在 [Runkit](https://runkit.com/icebob/moleculer-usage) 中运行这个例子试试

## 创建一个 Moleculer 项目

使用 [moleculer 脚手架](https://moleculer.services/docs/0.13/moleculer-cli.html) 创建一个基于moleculer的微服务项目

1. 全局安装 `moleculer-cli`

```shell
$ npm i moleculer-cli -g
```

2. 创建一个项目（可以命名为 moleculer-demo）

```shell
$ moleculer init project moleculer-demo
```

接下来会出现很多选项，可以直接按 Y 继续

3. 进入到 moleculer-demo 目录下

```shell
$ cd moleculer-demo
```

4. 启动服务

```shell
npm run dev
```

5. 在浏览器里访问 http://localhost:3000/ ，你会看到一个启动页面，页面中有两个链接，点击任意链接都可以通过 API 网关去访问 greeter service。

> 恭喜!
>
> 你已经成功你的创建了你的第一个基于 Moleculer 的微服务项目，下一步你可以在你的服务里检测我们的[示例](https://moleculer.services/docs/0.13/examples.html)或者 [demo 项目](https://github.com/moleculerjs/moleculer-examples)
