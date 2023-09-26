# Electron

## 什么是Electron

## 如何安装

1. **添加到Vue**

   通过命令以下命令来安装

   ```bash
   vue add electron-builder
   ```

   注意，有`node`版本的限制，**高版本可能无法安装**

2. **修改配置**

   在`vue.config.js`文件中修改：

   ```js
   module.exports = {
   	pluginOptions: {
       // 添加这里
   		electronBuilder: {
   			nodeIntegration: true,
         // 对于macOS，分别导出x64版本和Apple Silicon版本
   			builderOptions: {
   				artifactName: '${productName}-${version}-${os}-${arch}.${ext}',
   				mac: {
   					target: {
   						arch: ['x64', 'arm64'],
   						target: 'zip'
   					}
   				}
   			},
   		},
   	},
   }
   ```

## 设定窗口

- 窗口大小

  在`background.js`中设置，找到这里：

  ```js
  const win = new BrowserWindow({
    width: 1100,	// 这里是宽度
    height: 770,	// 这里是高度
    webPreferences: {
      nodeIntegration: process.env.ELECTRON_NODE_INTEGRATION,
      contextIsolation: !process.env.ELECTRON_NODE_INTEGRATION
    }
  }
  ```

  注意，不需要写`px`

- 设定窗口是否可以缩放

  同样是在`background.js`中设置，找到这里：

  ```js
  const win = new BrowserWindow({
    resizable: false,	// 在这里设置
    webPreferences: {
      nodeIntegration: process.env.ELECTRON_NODE_INTEGRATION,
      contextIsolation: !process.env.ELECTRON_NODE_INTEGRATION
    }
  }
  ```

- 设定沉浸式窗口栏

  也是在`background.js`中设置，找到这里：

  ```js
  const win = new BrowserWindow({
    titleBarStyle: 'hiddenInset',	// 在这里设置
    webPreferences: {
      nodeIntegration: process.env.ELECTRON_NODE_INTEGRATION,
      contextIsolation: !process.env.ELECTRON_NODE_INTEGRATION
    }
  }
  ```

  注意，这时候可能会导致窗口无法拖动，需要在窗口中增加一个可以拖动的块，如下

  ```vue
  <template>
      <div class="dragArea"></div>
  </template>
  
  <style scoped>
  .dragArea{
      position: fixed;
      top: 0;
      left: 0;
      height: 30px;
      width: 100%;
      -webkit-app-region: drag;
  }
  </style>
  ```

  另注意，窗口内容需要设置`margin-top`，如下：
  
  ```css
  .content{
    margin-top: 30px
  }
  ```
  

## 使用node组件

如果需要`node`组件，例如`fs`或者`path`等， 需要在`webPreferences`修改设置：

```js
win = new BrowserWindow({
		// 其它代码...
		webPreferences: {
			nodeIntegration:true,	// 这里修改为true
			contextIsolation:false,
		}
	})
```

