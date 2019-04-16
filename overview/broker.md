# Broker

Moleculer 最主要的组成就上 `ServiceBroker`。主要作用是处理服务、调用操作、发出事件并以及远程节点通信。每一个 Moleculer 节点都必须有一个 `ServiceBroker` 实例。

## 创建 broker

### 使用默认设置创建 broker:

```javascript
const { ServiceBroker } = require("moleculer");
const broker = new ServiceBroker();
```

### 使用自定义设置创建 broker:

```javascript
const { ServiceBroker } = require("moleculer");
const broker = new ServiceBroker({
    logLevel: "info"
});
```

### 创建一个带转发器，可以与其他节点通信的 broker

```javascript
const { ServiceBroker } = require("moleculer");
const broker = new ServiceBroker({
    nodeID: "node-1",
    transporter: "nats://localhost:4222",
    logLevel: "debug",
    requestTimeout: 5 * 1000,
    requestRetry: 3
});
```

## Broker 配置数据

broker 所有配置项如下表所示：

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| namespace | String | '' |  同一网络下分段节点的节点命名空间 |
| nodeID | String | hostname + PID | 节点唯一标识，同一个命名空间下必须是唯一值 |
| logger | Boolean/Object/Function | console | 日志工具，默认情况下，将日志打印到控制台，也可以配置使用外部记录器，例如：[Winston](https://github.com/winstonjs/winston) 或 [Pino](https://github.com/pinojs/pino)。 [查看更多](https://moleculer.services/docs/0.13/logging.html) |
| logLevel | String | info | 内置控制台记录器的日志级别（跟踪、调试、信息、警告、错误、致命）。 |


