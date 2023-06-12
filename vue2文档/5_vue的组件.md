# vue的组件

（这里的“组件”是个名词，不是动词，英文为：`components`）

## 组件的作用

vue将HTML的思路运用于网页，因此有时候需要将自己写的一个vue代码融入到另一个页面

## 使用组件

`子组件`可以根据需求定义：

```vue
<template>
	<div>
     <button @click="fun">这是按钮</button>
  </div>
</template>
<script>
  export default {
    methods: {
      fun:function(){
				console.log('Hello world!');
      }
    }
  }
</script>
```

`父组件`需要引入`子组件`

```vue
<template>
	<div>
    <childPart></childPart>
  </div>
</template>

<script>
  import childPart from '@/components/childPartView.vue';
  
  export default {
		components:{
        childPart
    },
  }
</script>
```

其中`components`也可以这样写：

```js
components:{
  "childPartTemplate":childPart
}
```

注意，这时候在父组件中使用的标签为`childPartTemplate`，因为你将`childPart`定义为`childPartTemplate`

## 子组件和父组件传递参数

### 父组建向子组件传递变量

使用`prop`向子组件传递变量，例如：
父组件：

```vue
<template>
	<div>
    <childPart :msg="variable"></childPart>
  </div>
</template>

<script>
  import childPart from '@/components/childPartView.vue';
  
  export default {
		components:{
        childPart
    },
    data(){
      return{
        variable: "Hello world!"
      }
    }
  }
</script>
```

注意，这里的`msg`是对于子组件的变量名称，而`variable`是父组件的变量名称
对于子组件：

```vue
<template>
	<div>
     <button>这是按钮</button>
  </div>
</template>
<script>
  export default {
    props: {
      msg: String
    }
  }
</script>
```

注意在`props`中要注明变量类型，例如`String`、`int`等，`data`中的变量不能与`props`重名，`props`中变量可以直接使用

### 子组件向父组件传递变量

使用`emit`向子组件传递变量，例如：

父组件：
```vue
<template>
	<div>
    <childPart @emitVariable="getVariable"></childPart>
  </div>
</template>

<script>
  import childPart from '@/components/childPartView.vue';
  
  export default {
		components:{
        childPart
    },
    data(){
      return{
        Variable: undefined
      }
    }
    methods: {
      getVariable:function(val){
        this.Variable=val;
      }
    }
  }
</script>
```

子组件：
```vue
<template>
	<div>
     <button @click="go">这是按钮</button>
  </div>
</template>
<script>
  export default {
    data(){
      return{
        msg: "Hello world!"
      }
    }
    methods: {
    	go:function(){
        this.$emit("emitVariable", this.msg)
      }
  	}
  }
</script>
```

### 父组件调用子组件中的函数

使用`ref`来调用子组件的函数

父组件：

```vue
<template>
	<div>
    <childPart ref="childRef"></childPart>
    <button @click="useChildFunction">这是一个按钮</button>
  </div>
</template>

<script>
  import childPart from '@/components/childPartView.vue';
  
  export default {
		components:{
        childPart
    },
    methods:{
      useChildFunction(){
        this.$refs.childRef.childFunction();
      }
    }
  }
</script>
```

子组件：

```vue
<template>
	<div>
     
  </div>
</template>
<script>
  export default {
    methods: {
    	childFunction(){
        // 子组件的函数
      }
  	}
  }
</script>
```

