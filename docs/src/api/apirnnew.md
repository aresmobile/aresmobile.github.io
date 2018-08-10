### 须知

#### 新版本宿主支持
本接口列表正在开发中，目前线上版本尚未支持，目前宿主正在配合改造，改造上线后，各业务bundle可以开始使用开发、部署

#### Promise通用返回值

|返回值|返回类型|说明|
|:-|:-|:-|
|status|int|>0表示成功，否则失败，失败信息存于message中|
|message|string|失败信息|
|data|任意类型|数据体,当数据为空时没有data，因而需要判断data不为undfined|

新的RN接口都只支持Promise，以下所有返回值都是成功情况下data中数据

### NativeModules.AresStorage.save
###### 接口功能

> 类似AsyncStorage，将数据本地持久化

###### 支持平台

> android/iOS

###### 请求说明

> Object

|请求值|请求类型|说明|
|:-|:-|:-|
|key|string|Key值|
|data|任意类型|数据|

###### 返回说明

> 无

###### 接口示例

```javascript
​    const res = await NativeModules.AresStorage.save({
        key: 'sessionId',
        data: {
            value: 'a'
        }
    })
    if (res.status > 0) {
        console.log("success")
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresStorage.load
###### 接口功能

> 类似AsyncStorage，将数据从本地读出

###### 支持平台

> android/iOS

###### 请求说明

> String

###### 返回说明

> 任意类型

###### 接口示例

```javascript
​    const res = await NativeModules.AresStorage.load('sessionId')
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresStorage.clear
###### 接口功能

> 类似AsyncStorage，将数据从本地清除

###### 支持平台

> android/iOS

###### 请求说明

> String

###### 返回说明

> 无

###### 接口示例

```javascript
​    await NativeModules.AresStorage.clear('sessionId')
```

### NativeModules.AresRouter.getRouter
###### 接口功能

> 根据门牌号获取门牌号数据

###### 支持平台

> android/iOS

###### 请求说明

> String

###### 返回说明

> Object

|返回值|返回类型|说明|
|:-|:-|:-|
|remote_file|string|url|
|uri|string|scheme://门牌号|
|vendor_file|string|h5依赖的其它库|
|properties|Object|属性数据|

###### 接口示例

```javascript
​    const res = await NativeModules.AresRouter.getRouter('sessionId')
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresRouter.push
###### 接口功能

> 跳转到指定门牌号，是NavtiveModules.extra.openUri的Promise版本

###### 支持平台

> android/iOS

###### 请求说明

> Object

|请求值|请求类型|说明|
|:-|:-|:-|
|key|string|Key值|
|value|Object|要传给指定模块的数据|

###### 返回说明

> 任意类型,NavtiveModules.extra.setResult设置的数据

###### 接口示例

```javascript
​    const res = await NativeModules.AresRouter.push({
        key: 'multistore',
        value: {

        }
    })
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresRouter.pop
###### 接口功能

> 关闭当前页面，是NavtiveModules.extra.close的Promise版本

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
​    await NativeModules.AresRouter.pop()
```

### NativeModules.AresRouter.launchPadWeb
###### 接口功能

> 千米Pad，加载1000.com

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
​    await NativeModules.AresRouter.launchPadWeb()
```

### NativeModules.AresDebug.setDebugParams
###### 接口功能

> 设置环境id, SV和灰度

###### 支持平台

> android/iOS

###### 请求说明

> Object

|请求值|请求类型|说明|
|:-|:-|:-|
|key|string|Key值。可取'gray', 'eid', 'sv','envId'|
|value|number|数据。当key为'gray'时，value为0或者1|

###### 返回说明

> 无

###### 接口示例

```javascript
​    await NativeModules.AresDebug.setDebugParams({
        key: 'sv',
        value: 8
    })
```

### NativeModules.AresDebug.getDebugParams
###### 接口功能

> 获取环境id, SV和灰度

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Object

|返回值|返回类型|说明|
|:-|:-|:-|
|sv|int|App支持的最低版本，默认App的sv|
|gray|boolean|切灰度环境, 默认false|
|eid|int|环境id, 默认2|

###### 接口示例

```javascript
​    const res = await NativeModules.AresDebug.getDebugParams()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresDebug.enterPlayground
###### 接口功能

> 进入调试中心

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
​    await NativeModules.AresDebug.enterPlayground()
```

### NativeModules.AresDebug.isDev
###### 接口功能

> App是否处于Debug模式

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Boolean

###### 接口示例

```javascript
​    const res = await NativeModules.AresDebug.isDev()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresDevice.getDevice
###### 接口功能

> App设备信息

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Object

|返回值|返回类型|说明|
|:-|:-|:-|
|uuid|string|设备唯一标识|
|deviceType|string|'phone', 'pad'|

###### 接口示例

```javascript
​    const res = await NativeModules.AresDevice.getDevice()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresWeChat.isInstalled
###### 接口功能

> 设备是否安装了微信

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Boolean

###### 接口示例

```javascript
​    const res = await NativeModules.AresWeChat.isInstalled()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresWeChat.auth
###### 接口功能

> 微信授权

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Object

|返回值|返回类型|说明|
|:-|:-|:-|
|code|string|授权码|
|appId|string|微信Key|
|secret|string|微信Secret|

###### 接口示例

```javascript
​    const res = await NativeModules.AresWeChat.auth()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AresSecurity.rsa
###### 接口功能

> RSA公钥加密

###### 支持平台

> android/iOS

###### 请求说明

> String

###### 返回说明

> String

###### 接口示例

```javascript
​    const res = await NativeModules.AresSecurity.rsa('123456')
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```
### NativeModules.AresSecurity.md5
###### 接口功能

> md5加密

###### 支持平台

> android/iOS

###### 请求说明

> String

###### 返回说明

> String

###### 接口示例

```javascript
​    const res = await NativeModules.AresSecurity.md5('123456')
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.AppInfo.get
###### 接口功能

> 获取App的信息如name、version、pid

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> Object

|返回值|返回类型|说明|
|:-|:-|:-|
|pid|number|工程id|
|name|string|app的名称|
|version|string|app的版本号|

###### 接口示例

```javascript
​    const res = await NativeModules.AppInfo.get()
    if (res.status > 0) {
        if (res.data != undefined) {
            console.log(res.data)
        }
    } else {
        console.log(res.message)
    }
```

### NativeModules.util.comment
###### 接口功能

> 打开app评分

###### 支持平台

> android/iOS

###### 请求说明

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
​    NativeModules.util.comment()
```
