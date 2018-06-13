

### 使用说明

本接口是RN Hybrid接口，通过调用所提供的js接口，来调用原生平台的能力，会自动根据js代码所运行的环境来判别调用iOS还是Android的对应功能。

> 比如，你想要在js代码中启动摄像头，只需要提供本文下面提供的对应js接口即可，它会自动启动移动端设备上的对应设备


### NativeModules.extra.close

###### 接口功能

> 关闭当前活动页

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
​	NativeModules.extra.close()
```

### NativeModules.extra.locate

###### 接口功能

> 选择地理位置

###### 支持平台

> android/iOS

###### 请求参数

> | 参数        | 参数类型   | 说明   |
> | :-------- | :----- | :--- |
> | title     | string | 标题   |
> | latitude  | double | 纬度   |
> | longitude | double | 经度   |

###### 返回说明

> | 参数     | 参数类型   | 说明      |
> | :----- | :----- | :------ |
> | error  | Object | 用户取消时有值 |
> | events | Object | 地理位置信息  |
> events示例
```
{
  latitude: 39.90338455564453,
  city: '北京市',
  adcode: '110105',
  address: '北京市朝阳区南磨房镇北京农商银行(通惠国际分理处)北京国家广告产业园区',
  title: '北京农商银行(通惠国际分理处)北京国家广告产业园区',
  longitude: 116.47355494577586,
  adName: '朝阳区',
  province: '北京市'
}
```
###### 接口示例

```javascript
NativeModules.extra.locate({
      title: '位置',
      latitude: 39.903578,
      longitude: 116.473565
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events)
      }
    })
```

### NativeModules.extra.getLocation

###### 接口功能

> 获取地理位置（后台获取，无界面）

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> | 参数     | 参数类型   | 说明      |
> | :----- | :----- | :------ |
> | events | Object | 地理位置信息  |
> events示例
```
{
  latitude: 39.90338455564453,
  address: '北京市朝阳区南磨房镇北京农商银行(通惠国际分理处)北京国家广告产业园区',
  longitude: 116.47355494577586,
}
```
###### 接口示例

```javascript
NativeModules.extra.getLocation({
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events.latitude)
        console.log(events.longitude)
        console.log(events.address)
      }
    })
```


### NativeModules.extra.openLink

###### 接口功能

> 新启动一个页面展示网页

###### 支持平台

> android/iOS

###### 请求参数

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | url   | string | 网页地址 |

###### 返回说明

无

###### 接口示例

```javascript
NativeModules.extra.openLink({
      url: 'http://www.qianmi.com',//
    }, (error, events) => {
    })
    
```

### NativeModules.extra.openUri

###### 接口功能

> 跳转指定uri的原生、h5或rn页

###### 支持平台

> android/iOS

###### 请求参数

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | key   | string | 工程门牌号 |
> | value | Object | 附带的数据 |

###### 返回说明

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | error   | string | 错误信息，调用失败情况下 |
> | events | Object | 附带的数据，下一个窗口返回给当前的数据，结构等同于NativeModules.extra.setResult参数 |

###### 接口示例

```javascript
NativeModules.extra.openUri({
      key: 'h5demo',
      value: {
        adminId: 'A1111'
      }
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events)
      }
    })
    返回值通常与NativeModules.extra.setResult 一起用
    adminId值即为this.props.adminId
```

### NativeModules.extra.setResult

###### 接口功能

> 关闭当前窗口，并返回数据给前一个窗口

###### 支持平台

> android/iOS

###### 请求参数

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | data   | Object | 要返回给上一窗口的数据 |

###### 返回说明

> 无

###### 接口示例

```javascript
NativeModules.extra.setResult({
      adminId: 12345
    })
```

### NativeModules.extra.startNavi

###### 接口功能

> 地图导航

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title| String    | 是| 标题|
| latitude| String    | 是| 纬度|
| longitude| String    | 是| 经度|
| address| String    | 是| 名称或地址|

###### 返回说明

> 无

###### 接口示例

```javascript
NativeModules.extra.startNavi({
      title: "导航",
      latitude: 39.978234, 
      longitude: 116.352792, 
      address: '目的地'
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events)
      }
    })
```

### NativeModules.extra.addMarker

###### 接口功能

> 地图标记

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title| String    | 是| 标题|
| locations| JSONArray    | 是| 内部类型同ares.extra.startNavi|

###### 返回说明

> 无

###### 接口示例

```javascript
NativeModules.extra.addMarker({
      title: "订单地图",
      locations: [
          { latitude: 39.992520, longitude: 116.336170, address: 'name1' },
          { latitude: 39.998293, longitude: 116.352343, address: 'name2' },
          { latitude: 40.004087, longitude: 116.348904, address: 'name3' },
          { latitude: 40.001442, longitude: 116.353915, address: 'name4' },
          { latitude: 39.989105, longitude: 116.353915, address: 'name5' },
          { latitude: 39.989098, longitude: 116.360200, address: 'name6' },
          { latitude: 39.998439, longitude: 116.360201, address: 'name7' },
          { latitude: 39.979590, longitude: 116.324219, address: 'name8' },
          { latitude: 39.978234, longitude: 116.352792, address: 'name9' }
      ]
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events)
      }
    })
```

### NativeModules.extra.share

###### 接口功能

> 应用间分享

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title| String    | 是| 标题|
| content| String    | 是| 分享的内容|
| image| String    | 否| 分享的logo，可以不传则默认为猫头鹰|
| url| String    | 是| 分享链接|
| sms| bool    | 否| 是否展示短信选项，用户点击后在回调中处理后续操作|
| grid| bool    | 否| 是否展示九宫格图片分享选项，用户点击后在回调中处理后续操作|
| poster| bool    | 否| 是否展示海报分享选项，用户点击后在回调中处理后续操作|
| type| String    | 否| 直接分享，可以不显示弹框直接发起分享操作，取值见"type取值"|
| miniApp| bool    | 否| 小程序分享专用，见“小程序分享”|
| userName| String    | 否| 小程序分享专用，见“小程序分享|
| path| String    | 否| 小程序分享专用，见“小程序分享|

###### type取值
qq/wechat/wechat_timeline/qzone/link/qrcode/sms/miniApp


###### 返回说明

> 无

###### 接口示例 - 常规分享

```javascript
NativeModules.extra.share({
      type:'qq'//直接分享到指定平台(wechat、wechat_timeline、qzone、link、miniApp、qrcode)，可以不传
      title: "导航",
      content: "rn 分享",
      image: "http://xxx.png"
      url: "https://www.qianmi.com",
      sms: true/false,
      grid: true/false,
      poster: true/false,
      type: "xxx"
    }, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        if (events && events.type == "sms") {
          alert("点击了短信")
        }
        if (events && events.type == "grid") {
          alert("点击了九宫格")
          // 调用九宫格图片分享API
        }
        if (events && events.type == "poster") {
          alert("点击了海报")
          // 自行处理海报操作
        }
      }
    })
```


###### 小程序分享

```javascript

NativeModules.extra.share({
            url: "http://wwww.qianmi.com",
            title: "demo",
            content: "demo test",
            miniApp:true,
            userName:"gh_1d17f63b7cbd",
            path:"/",
            image: "http://web-img.qmimg.com/qianmicom/u/cms/qianmi/201603/20132248iqr5.png",
        }, (error, events) => {})


```


### NativeModules.extra.shareMultiImages

###### 接口功能

> 分享多张图片到微信朋友圈（九宫格，最多9张图片，最少1张）

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| imageurls | String[]    | 是| 图片的地址数组|



###### 返回说明

> 无

###### 接口示例

```javascript
NativeModules.extra.shareMultiImages({
      imageurls: ["http://img.meifajia.com/o1aneipt09eCl5bqQp4ifbQdTHlKIJfq.jpg?imageView2/1/w/360/h/480/q/85",
      "http://img.meifajia.com/o1aneipt2fbZm38Zct4DH92p-ez7-fXt.jpg?imageView2/1/w/360/h/480/q/85",
      "http://img.meifajia.com/o1aneiocd24Y6jK8uQA8-8y-47H6vRe7.jpg?imageView2/1/w/360/h/480/q/85",
      "http://img.meifajia.com/o1aneiocdd94h6ld4kQJh8PcpjGSkORS.jpg?imageView2/1/w/360/h/480/q/85"
      ]
    },(error, events) => {
      if (error) {
        console.log(error)
      } else {
        console.log(events)
      }
    })
```

### NativeModules.extra.logout

###### 接口功能

> 退出登录（比如sessionId失效后跳转）

###### 支持平台

> android/iOS

###### 请求参数

> 无
###### 返回说明

> 无

###### 接口示例

```javascript
NativeModules.extra.logout()
```

### NativeModules.sessionStorage.set/get

###### 接口功能

> 临时存储，可以跨模块访问（app进程杀掉后擦除）

###### 支持平台

> android/iOS

###### 请求参数

> 无
###### 返回说明

> 无

```javascript
NativeModules.sessionStorage.set({
      key: "name",
      value: "john"
    }, (error, events) => {
      if (error) {
        console.log(error)
      }
    })
    
NativeModules.sessionStorage.get({key: "name"}, (error, events) => {
      if (error) {
        console.log(error)
      } else {
        alert(events)
      }
    })
```

### NativeModules.extra.setStore

###### 接口功能

> 选择一个店铺，在框架记录店铺信息(和enterRootActivity配合使用)

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| shopId| String    | 是| 店铺ID(adminId)|
| shopName| String    | 是| 店铺名称|
| sceneBname| String    | 是| 店铺Banme(场景Bname)|
###### 返回说明

> 无

```javascript
NativeModules.extra.setStore({
      shopId: "A1111111",
      shopName: "xxx的店铺",
      sceneBname: "cloudOrder"
    })
    
```

### NativeModules.extra.setSupplier

###### 接口功能

> 选择一个供应商，在框架记录供应商信息

###### 支持平台

> android/iOS

###### 请求参数

> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| supId| String    | 是| 供应商ID|

###### 返回说明

> 无

```javascript
NativeModules.extra.setSupplier({
    supId: xxxx
})
    
```

### NativeModules.extra.enterRootActivity

###### 接口功能

> 进入所选择店铺的工作台（必须先调用setStore）

###### 支持平台

> android/iOS

###### 请求参数

> 无
> 
###### 返回说明

> 无

```javascript
NativeModules.extra.enterRootActivity()
    
```

### NativeModules.extra.enterRootActivityRefresh

###### 接口功能

> 进入所选择店铺的工作台（带刷新）

###### 支持平台

> android/iOS

###### 请求参数

> 无
> 
###### 返回说明

> 无

```javascript
NativeModules.extra.enterRootActivityRefresh()
    
```


### NativeModules.UMAnalyticsModule<h3/>

###### 接口功能

> 友盟统计

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 无

###### 使用方式

```javascript
//为事件id打点 （最常用）
NativeModules.UMAnalyticsModule.onEvent("eventname")

//分类标签打点
NativeModules.UMAnalyticsModule.onEventWithLable("eventname","label")

//为当前事件的属性和取值（键值对），不能为空，如：{name:"umeng",sex:"man"}
NativeModules.UMAnalyticsModule.onEventWithMap("eventname",{name:"umeng",sex:"man"})

//数值用户每次触发的数值的分布情况，如事件持续时间、每次付款金额等
NativeModules.UMAnalyticsModule.onEventWithMapAndCount("eventname",{name:"umeng",sex:"man"},100);

```

### NativeModules.extra.setAndGetString<h3/>

###### 接口功能

> 本地数据存取，类似于RN提供的AsyncStorage

###### 支持平台

> android/iOS

###### 请求参数

> 见列表

###### 返回说明

> 无

###### 使用方式

```javascript
// get
NativeModules.extra.setAndGetString({
      type: 'get',
      key: 'common_function'
    },(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events)//获得返回值
        }
      })
      
// set
NativeModules.extra.setAndGetString({
      type: 'set',
      key: 'common_function',
      value: 'xxx'// 只支持string类型
    },(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events)
        }
      })
      
```

### NativeModules.extra.notificationSwitch<h3/>

###### 接口功能

> 推送通知开关

###### 支持平台

> android/iOS

###### 请求参数

> 见列表

###### 返回说明

> 无

###### 使用方式

```javascript
NativeModules.extra.notificationSwitch({
      sw: 'on'//'off'
    })
      
```

### NativeModules.extra.getUserInfo<h3/>

###### 接口功能

> 获取当前用户信息

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | error   | string | 错误信息，调用失败情况下 |
> | events | Object | 附带的用户数据 |

###### 使用方式

```javascript
NativeModules.extra.getUserInfo({
	},(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events.adminId)
          console.log(events.adminName)
          console.log(events.optId)
          console.log(events.optName)
          console.log(events.duserId)
          console.log(events.roleId)
          console.log(events.roleName)
          console.log(events.shopName)
          console.log(events.role)
          console.log(events.roleBName)
          console.log(events.sceneBName)
          console.log(events.ticketId)
          console.log(events.headUrl)
          console.log(events.nickName)
        }
      })
      
```


### NativeModules.extra.getModel<h3/>

###### 接口功能

> 获取设备型号

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | error   | string | 错误信息，调用失败情况下 |
> | events | String | 设备型号 |

###### 使用方式

```javascript
NativeModules.extra.getModel({
	},(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events)
        }
      })
      
```

### NativeModules.extra.playBeep<h3/>

###### 接口功能

> 播放声音（滴一下）

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 无

###### 使用方式

```javascript
NativeModules.extra.playBeep()
      
```

### NativeModules.extra.getContacts<h3/>

###### 接口功能

> 获取通讯录

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明


> | 参数    | 参数类型   | 说明    |
> | :---- | :----- | :---- |
> | error   | string | 错误信息，调用失败情况下 |
> | events | Array | 用户通讯录集合 |

###### 使用方式

```javascript
NativeModules.extra.getContacts({
},(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events)
        }
      })
      
```

### NativeModules.extra.wxMiniProgram<h3/>

###### 接口功能

> 打开小程序

###### 支持平台

> android/iOS

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| userName| String    | 是| 小程序原始id|
| path| String    | 是| 小程序界面的path|
###### 返回说明
> 无

###### 使用方式

```javascript
NativeModules.extra.wxMiniProgram({
	userName: 'gh_1f5f41405812',
    path: '/pages/business-card/index'
},(error, events) => {
        if (error) {
          console.log(error)
        } else {
          console.log(events)
        }
      })
      
```