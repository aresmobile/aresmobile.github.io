# Ares - 一个基于JsBridge的混合移动开发框架
>“我们不是为了超越Cordova和React Native，我们只是提供了另一种开发移动端的思路，让只会web开发的小伙伴们撸mobile，甚至连android/iOS的IDE都不用装，并且性能可接受”


npm install ares-mobile

## 总体规划图
<img src="http://7xtefp.com1.z0.glb.clouddn.com/WX20170209-145336@2x.png" width=518 height=220 />

**ares** 项目核心工程，包含js桥接代码和组件的android／iOS实现
> http://git.dev.qianmi.com/adminapp/ares

**ares-container** 宿主（webkit）工程，现已经整合到ares的andoid,ios目录中，也是提供了扫码方式的调试工程 
原始地址：
>http://git.dev.qianmi.com/adminapp/ares-container-android
>http://git.dev.qianmi.com/adminapp/ares-container-ios


**ares-kit** 提供出部分移动h5组件，方便快速开发和界面统一，用于千米电商云APP
> http://git.dev.qianmi.com/adminapp/ares-kit-web

**ares-publisher** 子功能地址、版本和发布系统，正在开发中

**ares-push** 子模块推送更新系统（规划中）

**ares-logger** 统一日志（规划中）

## Ares在千米电商云APP2.0中的应用

<img src="http://7xtefp.com1.z0.glb.clouddn.com/ares%20on%20adminapp.png" width=450 height=630/>

## 使用方法
[Why and How](doc/Tutorial.md)

## 客户端公开API列表
本API设计是参考了[钉钉开放平台](https://open-doc.dingtalk.com/doc2/detail?spm=0.0.0.0.s5srZu&treeId=171&articleId=104906&docType=1)的API格式（仅仅格式），目的在于将来可以快速的尽少修改的迁移到钉钉中
>例如使用ares.device.base.getUUID接口，会根据宿主环境自动适配到qm.device.base.getUUID或dd.device.base.getUUID

#### 设备
* device.base.getUUID 获取通用唯一识别码 (android,iOS)
* device.base.getInterface 获取热点接入信息(android,iOS)

#### 启动器
* device.launcher.checkInstalledApps  检测应用是否安装(android,iOS)
* device.launcher.launchApp 启动第三方应用(android,iOS)
* device.connection.getNetworkType 获取当前网络类型(android,iOS)

#### 弹窗
* device.notification.alert  alert (android,iOS)
* device.notification.confirm  confirm (android,iOS)
* device.notification.prompt  prompt  (android,iOS)
* device.notification.vibrat 震动 (android)
* device.notification.showPreloader （显示浮层，请和hidePreloader配对使用） (android,iOS)
* device.notification.hidePreloader hidePreloader (android,iOS)
* device.notification.toast  toast (android,iOS)
* device.notification.actionSheet 单选列表  (android,iOS)


#### 地图
* device.geolocation.get 获取当前地理位置 (android,iOS)
* device.geolocation.stop 停止获取当前地理位置，和get对应，需要在界面销毁的时候调用 (android,iOS)
* biz.map.view 展示位置 (android,iOS)

#### 业务
* biz.util.open 打开应用内页面(开发中开发中完善) (android,iOS)
* biz.util.datepicker 日期 (android,iOS)
* biz.util.timepicker 时间 (android,iOS)
* biz.util.openLink 在新窗口上打开链接 (android,iOS)
* biz.util.chosen  下拉单项选择（android,iOS）

#### 扫码
* biz.util.scan  扫描条形码、二维码 (android,iOS)

#### 分享
* biz.util.share  分享功能，目前支持：微信、微信朋友圈、QQ、QQ空间、支付宝、新浪微博、短消息 (android,iOS)

#### 电话
* biz.telephone.call  打电话 (android,iOS)

#### 导航栏
* biz.navigation.setMenu  设置菜单 (android,iOS)
* biz.navigation.setTitle  设置标题 (android,iOS)
* biz.navigation.setActionBar  设置导航栏整体,目前包含：显示/隐藏、返回显示／隐藏、背景色 (android,iOS)
