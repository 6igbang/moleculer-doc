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
| logFormatter | String/Function | 'default' | 内置控制台记录器的日志格式化程序。值：default, simple, short。也可以是一个函数。|
| logObjectPrinter | Function | null | 内置控制台记录器的阵列打印机（是一个自定义数据对象） |
| transporter | String/Object/Transporter | null | 转发器设置 [查看更多](https://moleculer.services/docs/0.13/networking.html) |
| requestTimeout | Number | 0 | 请求超时的时间，单位是毫秒，Disabled的时候是 0 |
| retryPolicy | Object | 请求重试策略设置，[查看更多](https://moleculer.services/docs/0.13/fault-tolerance.html#Retry) |
| maxCallLevel | Number | 0 | call level 限制，当达到最大上限的时候，broker 就会抛出一个 MaxCallLevelError 错误。（保护无限调用的情况） |
| heartbeatInterval | Number | 5 | 向其他节点发送心跳数据包的时间间隔（单位：秒）。 |
| heartbeatTimeout | Number | 15 | 将节点设置为不可用状态的等待时间（单位：秒）。 |
| tracking | Object | | 跟踪请求并在关闭前等待正在运行的请求。[查看更多](https://moleculer.services/docs/0.13/fault-tolerance.html) |
| disableBalancer | Boolean | false | 是否禁用内置请求和发出平衡器。如果是 Transporter，则必须是支持。 |
| registry | Object | | [Service Registry](https://moleculer.services/docs/0.13/registry.html) 的配置数据 |
| circuitBreaker | Object | | [Circuit Breaker](https://moleculer.services/docs/0.13/fault-tolerance.html#Circuit-Breaker) 的配置数据 |
| bulkhead | Object | | [bulkhead](https://moleculer.services/docs/0.13/fault-tolerance.html#Bulkhead) 的配置数据 |
| transit.maxQueueSize | Number | 50000 | 传输最大队列数？当有太多输出请求的时候，起到一个保护作用，防止内存的过度使用。当输出请求数量超过这个限制的时候，新的请求就会被拒绝，同时抛出一个 QueueIsfullError 错误。 |



## 全配置参数

```javascript
{
    namespace: "dev",
    nodeID: "node-25",

    logger: true,
    logLevel: "info",
    logFormatter: "default",
    logObjectPrinter: null,

    transporter: "nats://localhost:4222",

    requestTimeout: 5000,
    retryPolicy: {
        enabled: true,
        retries: 5,
        delay: 100,
        maxDelay: 1000,
        factor: 2,
        check: err => err && !!err.retryable
    },

    maxCallLevel: 100,
    heartbeatInterval: 5,
    heartbeatTimeout: 15,
    
    tracking: {
        enabled: true,
        shutdownTimeout: 5000,
    },

    disableBalancer: false,

    registry: {
        strategy: "RoundRobin",
        preferLocal: true
    },

    circuitBreaker: {
        enabled: true,
        threshold: 0.5,
        windowTime: 60,
        minRequestCount: 20,
        halfOpenTime: 10 * 1000,
        check: err => err && err.code >= 500
    },   

    bulkhead: {
        enabled: true,
        concurrency: 10,
        maxQueueSize: 100,
    },

    transit: {
        maxQueueSize: 50 * 1000,
        disableReconnect: false,
        packetLogFilter: []
    },     

    cacher: "memory",
    serializer: null,

    skipProcessEventRegistration: false

    validation: true,
    validator: null,

    metrics: true,
    metricsRate: 1,

    internalServices: true,
    internalMiddlewares: true,

    hotReload: true,

    ServiceFactory: null,
    ContextFactory: null,

    middlewares: [myMiddleware()],

    replCommands: [],

    created(broker) {
    },

    started(broker) {
    },

    stopped(broker) {
    }
}
```

