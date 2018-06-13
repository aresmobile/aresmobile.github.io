### 原理

每个bundle被宿主启动时，宿主都会以props的方式带一些常用的参数给bundle，业务可以通过props获取到常用的数据，比如登录的sessionId、环境变量

> 一个大致完整的props内容如下

```javascript

let props = {
    ticketId: 'qm16991sgA',
    serverStatus: 1,
    sceneName: 'onlineDistribution',
    sessionId: 'a3f3d4564347421ea9bee3a73f7906a8',
    custom: 0,
    adminId: 'A900975',
    envId: '2',
    roleName: '采购',
    sceneBName: 'onlineDistribution',
    longitude: '',
    username: '13218066562',
    uri: 'mypurchase',
    latitude: '',
    remote:
      'http://qianmi-resources.oss-cn-hangzhou.aliyuncs.com/ares/appci/D2PAPP/D2PAPP.0093269506119544.android.bundle',
    role: 'purchasing'
  }

  ```

  ### this.props.envId

###### 接口功能

> 获取当前环境id(在入口组件处获取)

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 返回0 - 6数字， 分别代表线上环境、测试1-5、性能环境

###### 接口示例

```javascript
var envId = this.props.envId
console.log(envId);
```

### this.props.sessionId

###### 接口功能

> 获取当前登录session id(在入口组件处获取)

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
var envId = this.props.sessionId
console.log(envId);
```

### this.props.username

###### 接口功能

> 获取当前登录者用户名(在入口组件处获取)

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> 无

###### 接口示例

```javascript
var username = this.props.username
console.log(username);
```

### this.props.sceneName

###### 接口功能

> 获取当前登录者所开通的场景名称(即bName, 在入口组件处获取)

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> String类型
> onlineDistribution（云订货）
> onlineMall（云商城）
> ？？？（社区店）

###### 接口示例

```javascript
var sceneName = this.props.sceneName
console.log(sceneName);
```

### this.props.longitude/latitude

###### 接口功能

> 获取当前地理位置经纬度，Android端并非GPS方式获取 ，会有误差(在入口组件处获取)
> this.props.longitude//经度；this.props.latitude//纬度

###### 支持平台

> android/iOS

###### 请求参数

> 无

###### 返回说明

> String类型（从double转换）

###### 接口示例

```javascript
var longitude = this.props.longitude
console.log(longitude);
```