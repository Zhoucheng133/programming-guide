# Electron

## 什么是Electron

## 如何安装

通过命令以下命令来安装

```bash
vue add electron-builder
```

注意，有`node`版本的限制，高版本可能无法安装

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

  
