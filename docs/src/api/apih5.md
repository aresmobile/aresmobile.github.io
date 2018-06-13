### ares.config ###

###### 接口功能
>jsapi配置

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|-----                               |
|jsApiList    | Array    |是|需要调用的jsapi列表，去掉'ares'开头                         |

###### 返回说明
> 无返回回调

###### 接口示例
> 申请在本页面可以掉用显示原生弹框和获取地理位置的接口

```javascript
ares.config({
    jsApiList: [
        'device.notification.alert',
    	'device.geolocation.get'
    ]
})
```

### 通过ares.ready接口处理成功验证 ###

ares.config调用后紧接着需要调用ares.ready接口，参数为回调函数，在环境准备就绪时触发，jsapi的调用需要保证在该回调函数触发成功后调用，否则无效

###### 接口功能
>ares.config接口的成功验证

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|-----                               |
|function    |function    |是|                         |


###### 返回说明
> 无

###### 接口示例

``` javascript
ares.ready(function () { })
```

### 在ares.ready的回调中立即执行api ###

jsapi必须要保证在ready成功后才能调用成功，然后ready是一个异步的过程，通知jsbridge和原生层夹在内存，如果紧跟着在ready函数后面调用jsapi（比如setTitle设置标题），可能会不成功。此时你需要在ready的回调函数中执行setTitle即可

###### 接口示例
```javascript
constructor(props){
	ares.ready(() => {
	    this.setTitle()
	 })
}

setTitle() {
        ares.biz.navigation.setTitle({
            title: "设置"
        })
    }
```

### 通过error接口处理失败验证 ###

ares.config验证失败会执行error函数，错误信息可以在返回的error参数中参看，下面为error信息示例:

```javascript
ares.error((error) => {
            this.setState({
                errorInfo: JSON.stringify(error),
                successInfo: '',
            })
        })
```

### 接口约定 ###

* 所有接口都为异步
* 接受一个object类型的参数
* 成功回调 onSuccess(某些异步接口的成功回调，将在事件触发时被调用，具体详情请查看相关onSuccess回调时机，未做描述的即为同步接口)
* 失败回调 onFail

```javascript
ares.命名空间.功能.方法({
    参数1: '',
    参数2: '',
    onSuccess: function(result) {
    //成功回调
    /*
    {
        //所有返回信息都输出在这里
    }*/
    },
    onFail: function(){
    //失败回调
    }
})
```


### ares.device.base.getUUID ###

###### 接口功能
> 获取通用唯一识别码

###### 支持平台
> android/iOS

###### 请求参数
>无

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| uuid    |string    |通用唯一识别码|

###### 接口示例

```javascript
ares.device.base.getUUID({
    onSuccess : function(data) {
        /*
        {
            uuid: '3udbhg98ddlljokkkl' //
        }
        */
    },
    onFail : function(err) {}
})
```

### ares.device.base.getInterface ###

###### 接口功能
> 获取热点接入信息

###### 支持平台
> android/iOS

###### 请求参数
>无

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| ssid    |string    |热点ssid|
| macIp    |string    |热点mac地址|

###### 接口示例

```javascript
ares.device.base.getInterface({
    onSuccess : function(data) {
        /*
        {
            ssid: 'alibaba-inc',
            macIp: '3c:12:aa:09'
        }
        */
    },
    onFail : function(err) {}
})
```

### ares.device.geolocation.get ###

###### 接口功能
> 获取当前地理位置

###### 支持平台
> android/iOS

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|-----                               |
| targetAccuracy    | Number   |是 |期望定位精度半径（单位米）|
| coordinate    |Number  |是  |1：获取高德坐标， 0：获取标准坐标；推荐使用高德坐标；标准坐标没有address字段|
| withReGeocode    |Boolean   |是 |是否需要带有逆地理编码信息，传false即可|

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| longitude    | Number    |经度|
| latitude    |Number    |纬度|
| address    |String    |地址|
>其他请参考具体log或[文档](https://open-doc.dingtalk.com/docs/doc.htm?spm=a219a.7629140.0.0.EMPEpr&treeId=171&articleId=104917&docType=1)

###### 接口示例

```javascript
ares.device.geolocation.get({
            targetAccuracy: 200,
            coordinate: 1,
            withReGeocode: false,
            onSuccess: function (data) {
                console.log('testGetGeoLocation: ')
                console.log(data)
            },
            onFail: function (error) {
                console.log(error)
            }
        })
```

### ares.device.geolocation.stop ###

###### 接口功能
>停止获取当前地理位置，和get对应，需要在界面销毁的时候调用(组件销毁时)


###### 支持平台
> android/iOS

###### 请求参数
> 无

###### 返回说明
> 无

###### 接口示例

```javascript
ares.device.geolocation.stop({
            onSuccess: function (data) {
                console.log('stopGetGeoLocation: ')
                console.log(data)
            },
            onFail: function (error) {
                console.log(error)
            }
        })
```

### ares.biz.map.view ###

###### 接口功能
>另启界面，在地图上展示地址位置

###### 支持平台
> android/iOS

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|-----                               |
| latitude    | Number   |是 |经度|
| longitude    |Number  |是  |纬度|
| title    |String   |是 |地址名|

###### 返回说明
> 无

###### 接口示例

```javascript
ares.biz.map.view({
            latitude: 39.903578, // 纬度
            longitude: 116.473565, // 经度
            title: "北京国家广告产业园" // 地址/POI名称
        })
```

### ares.biz.util.scan ###

###### 接口功能
> 扫描条形码、二维码

###### 支持平台
> android/iOS

###### 请求参数
>无

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| text    |string    |二维码/条形码数据|

###### 接口示例

```javascript
ares.biz.util.scan({
    onSuccess : function(data) {
        //返回扫码结果
        console.info(data.text)
    },
    onFail : function(err) {}
})
```

### ares.biz.pay.alipay ###

###### 接口功能
>  支付宝支付

###### 支持平台
> android/iOS

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| payInfo    |string    |是|支付宝appId、支付信息，<a href="https://doc.open.alipay.com/docs/doc.htm?spm=a219a.7629140.0.0.DoG5ZX&treeId=204&articleId=105300&docType=1" target="_payInfo">详情可见支付宝开放平台]|

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| resultStatus    |string    |支付结果返回状态：9000为支付成功|
| result    |string    |支付结果信息|
| memo    |string    |描述信息|

###### 接口示例

```javascript
ares.biz.pay.alipay({
    payInfo: "app_id=2016082001775904&biz_content=%",
    onSuccess : function(data) {
        //返回支付结果
        console.info(data)
    },
    onFail : function(err) {}
})
```

### ares.biz.pay.wechatPay ###

###### 接口功能
>  微信支付

###### 支持平台
> android/iOS

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| payInfo    |object    |是|支付信息，详情见<a href="https://pay.weixin.qq.com/wiki/doc/api/app/app.php?chapter=8_5">文档</a>|

###### 返回说明
> |参数|参数类型|说明|
|:-----  |:-------|:-----|
| resultStatus    |string    |支付结果返回状态|
| result    |string    |支付结果信息|

###### 接口示例

```javascript
ares.biz.pay.wechatPay({
    payInfo: {
        partnerid: '',
        prepayid: '',
        noncestr: '',
        timestamp: '1431564564',
        package: '',
        sign: ''
    },
    onSuccess: (response) => {
        alert(response.resultStatus+response.result);
    },
    onFail: function (err) {
        alert(err.errorCode+"    "+err.message);
    }
})
```

### ares.biz.telephone.call ###

###### 接口功能
>  拨打电话

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| phone    |string    |是|电话号码|

###### 返回说明
> 无

###### 接口示例

```javascript
ares.biz.telephone.call({
            phone: "18800008888", // 电话号码
        })
```


### ares.biz.navigation.setActionBar ###

###### 接口功能
>  导航栏属性设置

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| backgroundColor    |string    |否|背景颜色:"#ADD8E6"|
| show    |boolean    |否|导航栏显示或隐藏|
| back    |boolean    |否|显示返回键与否|

###### 返回说明
> 无

###### 接口示例

```javascript
ares.biz.navigation.setActionBar({
    show:false,//是否显示actionbar，默认显示
    back:false,//是否显示返回键，默认显示
    close:false,//是否显示返回键，默认显示
    backColor:"#ff0000",//返回键和close键颜色
    backgroundColor:"#00ff00",//actionbar背景色
})
```

### ares.biz.navigation.setMenu ###

###### 接口功能
>  导航栏设置菜单

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| backgroundColor    |string    |否|菜单图标背景颜色:"#ADD8E6"|
| textColor    |string    |否|字体按钮颜色:"#ADD8E6"|
| items    |array    |是|菜单信息|
| item.id   |string    |是|菜单id|
| item.iconId   |string    |否|菜单字体图标名称:<a href="http://pic.qianmi.com/app/doc/font/demo_fontclass.html" target="iconfont">可见默认字体库</a>或者自定义字体库(在android宿主项目assets新建font文件目录,将iconfont.ttf文件放在该目录下即可)|
| item.text    |string    |否|菜单名称|

###### 返回说明
>|参数|参数类型|说明|
|:-----  |:-------|:-----|
| id   |string    |菜单id|

###### 接口示例

```javascript
ares.biz.navigation.setMenu({
            backgroundColor: "#00FF00",
            textColor: "#ADD8E6",
            items: [
                {
                    "id": "1",//字符串
                    "iconId": "file",//字符串，图标命名
                    "text": "帮助"
                },
                {
                    "id": "2",
                    "iconId": "photo",
                    "text": "dierge"
                }
            ],
            onSuccess: function (data) {
                console.info(data.id)
            }
        })
```

### ares.biz.navigation.setTitle ###

###### 接口功能
>  导航栏设置标题

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title    |string    |是|标题|
| textColor    |string    |否|标题颜色:#FF00FF|

###### 返回说明
>无

###### 接口示例

```javascript
ares.biz.navigation.setTitle({
    title: "设置",
    textColor: "#FF00FF"
})
```

### ares.device.notification.alert ###
###### 接口功能
>  弹警告框

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| message |string    | 否| 内容|
| title    |string    |否 | 标题|
| buttonName |string    |是 | 按钮名称|

###### 返回说明
>无
###### 接口示例
```javascript
    ares.device.notification.alert({
	    message: "亲爱的",
	    title: "提示",//可传空
	    buttonName: "收到",
	    onSuccess : function() {
	        //onSuccess将在点击button之后回调
	        /*回调*/
	    },
	    onFail : function(err) {}
	});
```

### ares.biz.util.uploadImage ###
###### 接口功能
>  上传图片

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| multiple| boolean    | 是| 是否允许多选|
| max| int    | 是| 多选数量|
| clip| boolean    | 否| 是否需要裁剪|
| oval| boolean    | 否| 裁剪成圆|
| ratio| String    | 否| 裁剪比例|

###### 返回说明
>|参数|参数类型|说明|
|:-----  |:-------|:-----|
| onSuccess |JSONArray | 成功的urls|
| onFail |JSONObject | 失败或取消|

###### 接口示例
```javascript
  ares.biz.util.uploadImage({
            multiple: true,
            max: 1,
            clip: true,
            // oval: true,
            ratio: "35:21",
            onSuccess: function (data) {
                console.log(data)
            },
            onFail: function (error) {
                console.log(error)
            }
        })
```

### ares.device.notification.confirm ###
###### 接口功能
>  弹确认框

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| message |string    | 否| 内容|
| title    |string    |否 | 标题|
| buttonLabels |string[]    |是 | 按钮名称|

###### 返回说明
>|参数|参数类型|说明|
|:-----  |:-------|:-----|
| buttonIndex |int | 被点击按钮的索引值|

###### 接口示例
```javascript
 ares.device.notification.confirm({
    message: "退出登陆吗？",
    title: "提示",
    buttonLabels: ['取消', '退出'],
    onSuccess : function(result) {
        //onSuccess将在点击button之后回调
        /*
        {
            buttonIndex: 0 //被点击按钮的索引值，Number类型，从0开始
        }
        */
    },
    onFail : function(err) {}
});
```

### ares.biz.util.openlink ###
###### 接口功能
>  跳转到指定的链接

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| url|string    | 是| 地址|

###### 返回说明
无
###### 接口示例
```javascript
  ares.biz.util.openLink({
            url: 'http://www.baidu.com'
        })
      
```

### ares.extra.openUri ###
###### 接口功能
>  跳转到指定的模块

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| key|string    | 是| 内容|
| value    | JSONObject    |否 | 标题|

###### 返回说明
无
###### 接口示例
```javascript
  ares.extra.openUri({
     key: "shengyi",    
     value:{
         pointId:'a123',
         userId:'aaaa',
         userName:'hahaha'
     }
 })
//key的值即模块的门牌号，value是跳转需要带的参数
```



### ares.extra.logout ###
###### 接口功能
>  退出登录

###### 支持平台
> android/ios

###### 请求参数
无
###### 接口示例
```javascript
  ares.device.notification.confirm({
      message: "确定要退出登录吗？",
       title: "提示",
       buttonLabels: ['取消', '退出'],
       onSuccess : function(result) {
           if(result.buttonIndex == 1){
               ares.extra.logout({})  //退出登录
           }
       },
       onFail : function(err) {}
   });
//这里是弹框确认后退出
```

### ares.extra.version ###
###### 接口功能
>  获取版本号

###### 支持平台
> android/ios

###### 请求参数
无
###### 接口示例
```javascript
  ares.extra.version({
     onSuccess: (version) => {
         alert(version); //成功获取版本号
     },
     onFail: function (err) {
         alert(err.message);
     }
 })
```

### ares.extra.setResult ###
###### 接口功能
>  数据回调

###### 支持平台
> android/ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| data| JSONObject    | 是| 内容|

###### 接口示例
```javascript
  ares.extra.setResult({
      latitude : 'h5 测试纬度',
      longitude : 'h5测试经度',
      address : '测试地址',
      adminId: 123456
  })
```

### window.Server.getEnvId() ###
###### 接口功能
>  数据回调

###### 支持平台
> android/ios

###### 请求参数
> 无

###### 接口示例
```javascript
  var envId = window.Server.getEnvId()
  alert(envId)
```

### ares.extra.startNavi ###
###### 接口功能
>  地图导航

###### 支持平台
> ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title| String    | 是| 标题|
| latitude| String    | 是| 纬度|
| longitude| String    | 是| 经度|
| address| String    | 是| 名称或地址|

###### 接口示例
```javascript
  ares.extra.startNavi({
            title: "导航",
            latitude: 39.978234, 
            longitude: 116.352792, 
            address: '目的地'
            ,
            onSuccess : function(result) {
                
            },
            onFail : function(err) {

            }
        })
```

### ares.extra.addMarker ###
###### 接口功能
>  地图标记

###### 支持平台
> ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| title| String    | 是| 标题|
| locations| JSONArray    | 是| 内部类型同ares.extra.startNavi|

###### 接口示例
```javascript
  ares.extra.addMarker({
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
            ],
            onSuccess : function(result) {
                
            },
            onFail : function(err) {

            }
        })
```

### ares.extra.setAndGetString ###
###### 接口功能
>  存储字符串到本地和从本地读取字符串

###### 支持平台
> ios

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| type| String    | 是| 读取还是存储|
| key| String    | 是| 标记字符串|
| value| String   | 否| type 为 ‘set’，value不填，清空这个key对应的值|

###### 接口示例
```javascript
    ares.extra.setAndGetString({//存储字符串
        type: "set",
        key: "test",
        value: "hello setAndGetString",
        onSuccess : function(result) {
            
        }
    })
    ares.extra.setAndGetString({//读取字符串
        type: "get",
        key: "test",
        onSuccess : function(result) {
            alert(result)
        }
    })
```

### ares.extra.getLifecycle ###

###### 接口功能
>  获取生命周期状态

###### 支持平台
> ios/android

###### 请求参数
> 无

> ###### 接口示例
```javascript
    ares.extra.getLifecycle({
    //probation 试用期; normal 正常周期; prepay 提前付费期; upcoming 即将到期(30天内到期); protect 打烊保护期; close 打烊期
                onSuccess: function(result){
                    Toast.info(result.lifecycle)
                }
            })
```


### ares.biz.util.share ###

###### 接口功能
>  分型

###### 支持平台
> ios/android

###### 请求参数
> title, url, image, content

> ###### 接口示例
```javascript
 ares.biz.util.share({
            title: "悄悄告诉你，有家好店!",
            url: this.state.url != '' ? this.state.url : DEFAULT_SHARE_URL,
            image: this.state.appLogo,
            content: "发现一家好店！货源充足品质好！批发再也不用烦！",
            onSuccess: (data) => {
                /**
                {
                     type: 'sms',
                     content: ''
                }
                **/
            }
        })
```

### ares.extra.wxMiniProgram ###

###### 接口功能
>  打开微信小程序

###### 支持平台
> ios/android

###### 请求参数
> |参数|参数类型|必须|说明|
|:-----  |:-------|:-----|:-----|
| userName| String    | 是| 小程序原始id|
| path| String    | 是| 小程序界面的path|


> ###### 接口示例
```javascript
    ares.extra.wxMiniProgram({
            userName: 'gh_1f5f41405812',
            path: '/pages/business-card/index',
        })
```