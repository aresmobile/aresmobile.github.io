### 环境安装
```bash
#在package.json的dependency加入"@qianmi/ares-cli", "^0.1.6"
lerna bootstrap --registry http://registry.npm.qianmi.com
```

在package.json的<b>scripts</b>中加入下列命令

```json
"ares-init": "node node_modules/@qianmi/ares-cli/index.js --init",
"ares-init-ios": "node node_modules/@qianmi/ares-cli/index.js --init=ios",
"ares-init-android": "node node_modules/@qianmi/ares-cli/index.js --init=android",
"ares-ios": "node node_modules/@qianmi/ares-cli/index.js --ios --simulator 'iPhone 6'",
"ares-android": "node node_modules/@qianmi/ares-cli/index.js --android"
"ares-run-ios-simulator": "node node_modules/@qianmi/ares-cli/index.js --ios --runOnly --simulator 'iPhone 6'",
```

|命令|说明|
|:-----  |:-------|
| ares-init |  下载宿主工程代码到本地container目录  |
| ares-init-ios |  同上（仅下载ios）  |
| ares-init-android | 同上（仅下载android）   |
| ares-ios |   调试ios，类似“react-native run-ios” |
| ares-android |  调试android，类似“react-native run-android”   |
| ares-run-ios-simulator |  启动ios模拟器  |

执行下载宿主工程代码到本地

```bash
npm run ares-init
```

或

```bash
npm run ares-init-ios
```

或

```bash
npm run ares-init-android
```

添加相关目录到项目根目录.gitignore，*(container目录下的宿主文件比较大，不应被提交到你的工程仓库中)*

```
...
container/*
...
```


### 调试Android

（基本流程和rn官网的调试流程一致）

首先启动一个android模拟器，推荐用

* android studio自带的模拟器
* genymotion模拟器

或者通过USB连接你的手机到电脑（保证手机和电脑在同一网段）

在你的项目根目录下执行<b>npm start</b>

```bash
> arestest@0.0.1 start /Users/cht/work/workspace/ares/arestest
> node node_modules/react-native/local-cli/cli.js start

Scanning 560 folders for symlinks in /Users/cht/work/workspace/ares/arestest/node_modules (15ms)
 ┌────────────────────────────────────────────────────────────────────────────┐
 │  Running packager on port 8081.                                            │
 │                                                                            │
 │  Keep this packager running while developing on any JS projects. Feel      │
 │  free to close this tab and run your own packager instance if you          │
 │  prefer.                                                                   │
 │                                                                            │
 │  https://github.com/facebook/react-native                                  │
 │                                                                            │
 └────────────────────────────────────────────────────────────────────────────┘
Looking for JS files in
   /Users/cht/work/workspace/ares/arestest


React packager ready.

Loading dependency graph, done.

```

出现如上画面说明react native的package server已经启动在8081端口

另启一个控制台同样到你的项目根目录，执行<b>npm run ares-android</b> ，耐心等待，即可将代码运行到我们的宿主上。其中将经历以下步骤：

1. 编译并安装宿主
2. 启动调试专属Activity
3. 加载本地8081端口的RN远程脚本并渲染

<b>【tips】:</b>

1. 以下命令可以代替摇晃手机显示dev menu
```bash
adb shell input keyevent 82
```

2. 第一次启动调试宿主的时候可能会显示提示授权overlay的权限提示，请打开

3. 偶尔会出现xxx keeps stopping的提示，可以直接点击“Close app”忽略，不影响调试

### 调试iOS

在你的项目根目录下执行

```bash
npm start
npm run ares-ios/ares-run-ios-simulator
```

之后的调试流程与rn官网一致