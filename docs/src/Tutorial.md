# Ares介绍

### 为什么不直接使用Cordova？
Cordova已经很成熟了，为什么我们还要重新造轮子？

* 我们希望主壳子及一级页面仍然是原生（Cordova适合纯Hybrid App）
* 我们有独立的原生(iOS、Android)团队（架子有我们专门维护，Cordova更适合纯前端团队）
* 写很多分散的Cordova plugin vs 集中实现原生功能，然后统一暴露出来(前者更适合前端团队的开发方式，而我们不需要前端团队自己写插件)
* Cordova 若干现成插件(真的能拿来就用吗？)
* 使用WebViewJavascriptBridge、JsBridge，相比使用Cordova，我们并没有做更多的工作
* 对接钉钉、微信
* 更多的问题...如webview缓存，团队合作问题，js(或html)发布

### 实现方式
1. 收集钉钉接口
2. 前端ares.js封装
3. 集中开发原生widget，并和钉钉的key对应，接收返回同样的参数

### 使用方式
#### 方式1 手机扫码调试
1. 新建本地业务h5项目，依赖ares-mobile、ares-uikit
2. 编写业务代码，使用ares对接原生功能
3. 启动服务，并生成地址二维码
4. 下载ares原生app到手机(由我们打包发到ftp)
5. 扫码调试(手机接电脑chrome或safari调试)

#### 方式2 项目调试
1. 本地安装ares-cli
2. 运行ares create新建业务方项目
3. 编写业务代码，运行ares run ios/andorid调试 