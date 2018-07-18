### AresMapView 

高德地图组件，可以在地图组件上绘制多个点（图片）

#### 导入

package.json加入

```json
"dependencies": {
		"@qianmi/ares-mapview": "^0.1.1",
	},
```

执行

```
yarn
```

#### 使用

```javascript
import AresMapView from '@qianmi/ares-mapview'

class xxx extends Component {

	render() {
		return (
			...
			<AresMapView style={{width: 300, height: 300}} data={[
            {
              title: '起点',
              latitude: 31.9,
              longitude: 118.7,
              images: ['http://pic.qianmi.com/app/adminapp/img/start.png']
            },
            {
              title: '骑手',
              latitude: 31.93,
              longitude: 118.72,
              images: [
                'http://pic.qianmi.com/app/adminapp/img/peisong.png'
              ]
            },
            {
              title: '终点',
              latitude: 31.977355,
              longitude: 118.761388,
              images: ['http://pic.qianmi.com/app/adminapp/img/end.png']
            }
          ]}/>
		)
	}

}

```

图片需要传在线图片


### AresWebView

用于替代RN提供的webview，可以用来调用H5的ARES API


#### 导入

package.json加入

```json
"dependencies": {
		"@qianmi/ares-webview": "^0.1.1",
	},
```

执行

```
yarn
```


#### 使用

```javascript
import AresWebview from '@qianmi/ares-webview'

class xxx extends Component {

	render() {
		return (
			...
			<AresWebview 
			   style={{marginBottom: 20, width: 300, height: 600}} 
			   src={"http://qianmi-resources.oss-cn-hangzhou.aliyuncs.com/ares/appci/boss/multistore.73a35fe94507417c9c2e.html"}
			   />

		)
	}

}

```

