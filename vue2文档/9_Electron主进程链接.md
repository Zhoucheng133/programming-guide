# Electron主进程链接

*注意，在HTML页面中不允许进行`跨域访问(Cross-access)`，也就是不允许进行类爬虫的操作，但是使用Electron客户端可以

## 页面调用Electron主进程函数

注意，以下内容基于Vue2 + Electron的实现，根据具体情况来进行修改

对于页面端：
```vue
<template>
	<div>
  	<button @click="mainMethod">调用主进程函数按钮</button>
  </div>
</template>

<script>
  // 确保导入了ipcRenderer
  import { ipcRenderer } from 'electron';
  export default{
    beforeDestroy(){
      // 在组件销毁前设置标志位为 true
      this.isDestroyed = true
    }
    data(){
      return {
        isDestroyed: false,
        // 下面这个是需要传递的参数
        arg: "Hello world!"
      }
    }
    created(){
      // 对于主进程中的函数返回之后执行本页面中的什么函数
      ipcRenderer.on('ElectronMainResult', this.mainResult);
    },
    methods:{
      mainResult(){
        console.log("完成执行");
      },
      mainMethod(){
        ipcRenderer.send('ElectronMain', this.arg);
      }
    }
  }
</script>

<style scoped>
  /* ... */
</style>
```