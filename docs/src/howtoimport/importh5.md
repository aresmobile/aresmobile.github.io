### 原理 ###

我们通过在自定义的Webview中植入了一个javascriptbirdge，并且通过拦截iframe更新url的方式，在自定义的协议的基础上完成了native代码和js代码的交互

所有接口的调用成功与否的前提，是你的页面必须要跑在千米app/云小店app等运用ares搭建的宿主中，如果在微信或者别的浏览器中，是没有效果的

### 通过npm引入

在package.json中加入下列依赖

```javascript
  "dependencies": {
    "ares-mobile": "0.1.7",
    ...
  }
```

js代码中import项目

```javascript
import ares from 'ares-mobile'
```

### 通过html的script引入

在body中加入下列代码

```html
<script src="http://pic.qianmi.com/app/adminapp/ares/1/bundle.js"></script>
```

### 举例使用
1. 按照上步骤引入bundle.js
2. 使用ares.config注册biz.util.openLink函数
3. 使用ares.ready通知注册
4. 判断useragent，如果运行在app中，通过openLink来跳转新的连接（需要先执行ares.ready）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
    <title>Ares</title>
</head>
<body style="background-color: #f0f0f0;">
<div id="root"></div>
<script src="http://pic.qianmi.com/app/adminapp/ares/1/bundle.js"></script>
<script>
	ares.extra.add('openUri')
    ares.config({
            jsApiList: [
                'biz.util.openLink',
                'extra.openUri'
            ]
        })
    ares.ready(function () {
        ares.biz.util.openLink({
            url: 'http://www.baidu.com'
        })//只要保证ares.ready先执行即可
        ares.extra.openUri({
            key: "personcert",    
            value:{}
        })//跳个人认证
    })
    
</script>
<div id="root "></div>
</body>
</html>

```