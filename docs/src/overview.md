# 总体介绍和架构

## 设计目的
我们可以把APP分为两种

* 第一种是单线索型，app的所有业务一个团队来设计开发，一个团队负责控制上架、版本等工作，内部高耦合
* 第二种是多线索型，app的所有业务分散在不同的团队，彼此之间内部高耦合，外部低耦合，模块化设计，所有模块汇聚到一起形成一个应用。

电商型APP就是典型的第二种，我们可以认为订单、商品、采购、会员、支付等等都是由不同的业务团队专业性的负责。为了开发这么一种APP需要一种能够支撑模块化开发的架构设计，即组件化、插件化（此“组件”非React 中的Component的概念，而是一个可直接使用的大组件，比如整个采购流程）。市面上的DroidPlugin、Nuwa、Small、Atlas等等都是为了解决此类问题而诞生的框架。而上述框架都是基于原生开发的，需要每个模块都是一个可运行的原生子app，开发成本依然很高。

随着React Native和H5(Hybrid技术)等流行，在既不增加开发成本，也不大幅度降低运行性能的前提下，我们期望我们设计的框架能够达到下列标准，否者就是失败的：

* 团队之间解耦，独立开发，互不干扰，
* 开发者只需要很少，甚至不需要了解android／iOS底层特性，专注于业务即可
* 子模块可以独立发布、升级、降级、维护
* 子模块运行性能高于普通H5的性能

目前来看，Ares框架已经达到了上述条件，当然需要经历项目的考验需要不断的优化。

## 总体设计
我们用一张图来描述基于Ares框架的APP是什么样的

<img src="http://7xtefp.com1.z0.glb.clouddn.com/ares%20on%20adminapp.png" width=450 height=630/>


1. 首先整个APP的登录、Home界面是原生的，这里承载了一个APP所有的基础设施，比如存储用户登录信息（session\token）、增强的webview、react native的承载activity/viewcontroller，以及各种各样的第三方库（支付、定位、地图、相机、扫码、电话、友盟等等）

2. 我们一个子模块，比如订单列表，开发者用H5或者React Native开发好后，将这独立的模块打包成js，上传到固定位置，同时在【Ares移动应用模块管理系统】中进行登记，产品经理在CRM上配置好菜单

3. APP在Home界面拿到订单列表的远程文件地址并预先下载，当用户点击该功能时，根据【实现方式】来启动增强webview或者reactActivty/Viewcontroller来渲染界面

4. 当订单列表需要升级的时候，只需要重新打包并上传即可，【Ares移动应用模块管理系统】自动感知新版本，项目经理只要在【Ares移动应用模块管理系统】上点击【部署】，客户手上的APP即接受到更新，APP无需重新发布上架

**形象的说，APP只是一层皮。**
我们拿电商云来举例，电商云控制台PC版本就是一层皮，我们用react开发PC界面，研发来开发业务接口，然后在这层PC界面上调用业务接口，让这层皮有血有肉。而APP我们认为是另一种皮（比如是个黑种人？），我们要达到的目的就是让开发者只要会PC的前端开发的基础上就能快速的开发这层皮，并且复用同样的血肉（即接口）。电商云控制台PC目前就是合作式开发的，但是每个子模块是直接链接过去的，子模块之间共享session。而电商云APP则是把子模块下载下来，用合适的【解释器】来运行以渲染出界面。话说回来，浏览器本身就是个【解释器】，那么我们可以把电商云APP比喻成浏览器。而电商云APP里面的Home菜单可以形象的比喻成浏览器中的【书签夹】


## 架构设计

Ares框架并不是一个单一的项目，是几种项目的结合体，这里有移动端底层的封装、增强的webview、jsbridge模块、应用模块管理系统等等，总体设计图如下：

<img src="http://7xtefp.com1.z0.glb.clouddn.com/WX20170209-145336@2x.png" width=600 height=240 />

**ares** 项目核心工程，包含jsbridge代码和H5调用原生组件的android／iOS实现，以及React Native的项目依赖以及相关库
> http://git.dev.qianmi.com/adminapp/ares

**ares-container** 宿主（webkit）工程，现已经整合到ares的andoid,ios目录中，也是提供了扫码方式的调试工程 
原始地址：
>http://git.dev.qianmi.com/adminapp/ares-container-android

>http://git.dev.qianmi.com/adminapp/ares-container-ios


**ares-kit** 提供出部分移动h5组件，方便快速开发和界面统一，用于千米电商云APP
> http://git.dev.qianmi.com/adminapp/ares-kit-web

**ares-publisher** Ares移动应用模块管理系统，负责子模块的发布、版本升级、降级等维护管理，充当了PC端类似于Bugatti的工作，前后端分离
> http://git.dev.qianmi.com/adminapp/ares-publisher-api

> http://git.dev.qianmi.com/adminapp/ares-publisher-front

**ares-push** 子模块推送更新系统，目的在于让APP能够实时监测到子模块的升级从而立即下载更新（规划中）

**ares-logger** 统一日志（规划中）


## 为什么不直接使用Cordova?
Cordova已经很成熟了，为什么我们还要重新造轮子？

* 我们希望主壳子及一级页面仍然是原生（Cordova适合纯Hybrid App）
* 我们有独立的原生(iOS、Android)团队（架子有我们专门维护，Cordova更适合纯前端团队）
* 写很多分散的Cordova plugin vs 集中实现原生功能，然后统一暴露出来(前者更适合前端团队的开发方式，而我们不需要前端团队自己写插件)
* Cordova 若干现成插件(真的能拿来就用吗？)
* 使用WebViewJavascriptBridge、JsBridge，相比使用Cordova，我们并没有做更多的工作
* 对接钉钉、微信
* 更多的问题...如webview缓存，团队合作问题，js(或html)发布
