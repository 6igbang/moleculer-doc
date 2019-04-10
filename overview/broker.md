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
