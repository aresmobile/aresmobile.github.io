### 原理

目前多个bundle之间的交互，一般通过openUri或者新的AresRouter.push去实现，A bundle启动B bundle，B bundle通过回调通知A bundle具体的数据结果。但是实际中很多需求通过这种方式不大方便实现，多个上下文（React Native或者H5）都是处于运行态、隔离的环境，彼此交互变的比较困难。

于是我们借用了EventBus的理念，实现了全局的<b>消息收发总线机制</b>，就像<b>蝴蝶效应</b>一样，取名为AresButterfly。

任何一个模块（可能是RN实现的业务，也有可能是H5的），只要在合适的位置（推荐在构造方法内）注册，其他任何模块发送的butterfly消息都可以接收到，两个模块之间约定好obj格式即可进行互动。

![butterfly](/docs/img/butterfly.png)

### for React Native

#### 注册接收

```javascript
import { DeviceEventEmitter } from 'react-native'

componentDidMount() {
    DeviceEventEmitter.addListener("onButterfly", msg => {
      console.log(JSON.stringify(msg))
      // parse the message and then do response
    })
  }
```

#### 发送消息
```javascript
import { NativeModules } from 'react-native'

NativeModules.AresButterfly.Post(msg)// msg is an object
```

### for H5

#### 注册接收

```javascript

 constructor(props) {
    super(props)

    //...
    ares.extra.add('butterflyRegister')
    ares.config({
      jsApiList: [
        'extra.butterflyRegister'
      ]
    })

    //...
 }

 componentDidMount(){
    ares.extra.butterflyRegister({
        onSuccess : function(msg) {
            // parse the message and then do response
        },
        onFail : function(err) {}
    })
 }
```

#### 发送消息

```javascript
constructor(props) {
    super(props)

    //...
    ares.extra.add('butterflyPost')
    ares.config({
      jsApiList: [
        'extra.butterflyPost'
      ]
    })

    //...
 }

 componentDidMount(){
    ares.extra.butterflyPost({
        msg : {
            // obj
        }
    })
 }
```
