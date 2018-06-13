### 原理

我们基本上是完全复用了react-native官方提供的jsbridge的能力，将各种本地能力扩展了各种module供业务调用

所有接口的调用成功与否的前提，是你的页面必须要跑在千米app/云小店app等运用ares搭建的宿主中，跑到别的app或者是你自己通过react-native init创建的demo中，是没有效果的

### 原生模块的调用

这是最常用的调用方式，基本原理是通过js触发native代码的执行，同时接收回调结果（部分支持promise格式）

```javascript
import { NativeModules } from 'react-native';

NativeModules.xxx.yyy()

```

### 原生UI组件的使用

部分UI组件（比如AresWebview）被再次封装成了RN可调用的方式

### 事件监听

当一些原生事件发生时，比如离线状态、即时推送到来等等，可以将相关事件发送至react native上下文，只需通过DeviceEventEmitter即可实现监听

```javascript

// 例如onAppPush这个事件
import { DeviceEventEmitter } from 'react-native'

componentDidMount() {
    DeviceEventEmitter.addListener("onAppPush", data => {
      console.log(JSON.stringify(data))
      // do something for example refresh
    })
  }

```