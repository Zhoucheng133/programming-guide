# vue项目的结构

- `assets`：用于存储各种其他文件组件（例如图片）
- `components`：用于存储各种页面的组件
- `router`：用于存储router数据
- `views`：用于存储各种文件
- `App.vue`：一个vue界面从这里开始
- `main.js`：多数情况下在这里导入各种模组

## 文件引用

在vue项目中可以使用`../xxx/xxx`这样的文件引用方式，也可以使用`@/xxx/xxx`，其中`@`表示从`src`文件夹
