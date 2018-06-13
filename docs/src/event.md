
### onAppPush（即时推送事件）###

###### 接口功能

可以让RN上下文接收到即时推送（基于极光推送长连接通道）事件，支持传递参数。比如如下场景：名片夹小程序修改了用户名，可以实时通知让app上的某个RN实现的界面立即刷新。

###### 对接方法

* 当事件发生时，bff接口去调用极光的推送API，传递具体的数据，后端demo如下：

```javascript

var fetch = require('node-fetch');
//每一个鉴权对应一个app，需要单独发送一次 (AppKey:Master Secret)
// var b = new Buffer('00c396a7f505e73acb0fb459:ee5ef57eeea6289990fd2e41')//千米APP企业分发鉴权
var b = new Buffer('f4dfcf5a8d4d514e7292347e:b3c1408ed742734476ce819f')//千米APP鉴权
// var b = new Buffer('197d94a18f27c510e322e86c:a8374f1ed9b4922e3122595d')//云小店APP鉴权
// var b = new Buffer('41c62872e9df183544585891:4a39376c48c4b7f600f94373')//云小店HD（android）鉴权
var auth = b.toString('base64')
var url = 'https://api.jpush.cn/v3/push'

var body = {
    platform:"all",
    audience:{
            alias: ["qm10033sex"]
        },
    message: {
        msg_content: "custom_content",//可任意填写，不可忽略
        content_type: "rnpush",//可任意填写，可忽略
        title: "msg",//可任意填写，可忽略
        extras: {//传输的数据
            key: "value",
            name: "jack"
        }
    },
    options: {
        time_to_live: 60,
        apns_production: false
    }
}

fetch(url,{
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': 'Basic ' + auth
        },
    body: JSON.stringify(body)
}).then(res => {
    console.log(res.status + ":" + res.statusText)
}).catch(error => {
    console.log(error)
})

```

其中audience为你希望谁去接收（此时登录app的这个人的ticketId，可支持多人），message.extras字段为实际希望传输给RN界面的参数。

具体可以参考[jpush_demo](http://git.dev.qianmi.com/adminapp/jpush_demo)

运行*npm run test -- push*以发送一个测试的通知，注意修改对应的appkey(Buffer)和接收人audience

* RN业务界面如何接收

```javascript

import { DeviceEventEmitter } from 'react-native'

componentDidMount() {
    DeviceEventEmitter.addListener("onAppPush", data => {
      console.log(JSON.stringify(data))
      // do something for example refresh
    })
  }

```

打印出结果{"key":"value","name":"jack"}