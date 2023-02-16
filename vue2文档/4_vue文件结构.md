# vue文件结构

## 页面结构

```vue
<template>
	<div>
    
  </div>
</template>
```

这是对于一个基本的vue文件应有的内容，其中`div`在`template`标签下一层<mark>**只允许有一对**</mark>

`div`标签下的内容同一般的`HTML`语法

## script结构

```vue
<script>
export default {
    data() {
        return {
					
        }
    },
    components:{
        
    },
    mounted() {

    },
    watch: {

    },
    methods: {

        }
    },
  	created: {
      
    },
    props:{
      
    }
}
</script>
```

- `data`
  
  这一部分用于存储`变量`
  注意，`data`下必须有`return`，<mark>**所有变量写在`retrun`中**</mark>
  变量形式为`json`，具体如下：  
  
  ```js
  data() {
    return{
      text1: "hello world!",
      text2: "hello vue!"
    }
  }
  ```
  
  注意，所有变量最后都有`,`（英文逗号），最后一行可以没有
  
- `components`
  这一部分用于存储`子组件`
  详细内容见：`5_vue的组件`章节

- `mounted`
  这一部分用于存储`钩子函数`
  这一部分的函数自动运行，不需要手动调用

- `watch`
  这一部分用于存储`监听变量的函数`
  使用方法如下（监听`text`变量）：

  ```js
  watch: {
    text: function(newVal,oldVal){
    	console.log('新的值为',newVal);
      console.log('旧的值为',oldVal);
    }
  }
  ```

- `methods`
  这一部分用于存储`函数`
  使用方法为

  ```js
  methods: {
  	add: function(){
      this.text+="hello!"
    },
  }
  ```

  或者也可以这样使用
  ```js
  methods: {
  	add(){
      this.text+="hello!"
    },
  }
  ```

- `created`
  这一部分用于存储的是`页面加载完成后执行的代码`
  可以调用`method`中的代码
  
- `props`
  这一部分用于存储的是`父组件的变量`，详细见：`5_vue的组件`章节

## style结构

vue有两种`style`结构，其中一个是一般的`style`

```vue
<style>
  
</style>
```

这样会出现一个问题，就是样式穿透，如果导入了组件，会修改组件的样式

因此使用这样的标签可以防止穿透：
```vue
<style scoped>
  
</style>
```

但是<mark>不能</mark>用于：`body`、`div`等全局的标签，例如（<mark>错误示范！</mark>）：

```vue
<style scopped>
  body{
    margin: 0;
  }
</style>
```
