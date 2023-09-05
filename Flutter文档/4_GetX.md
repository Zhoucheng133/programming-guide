# GetX

GetX是一个在`Flutter`创建全局变量的库

## 安装

在项目的命令行中执行：

```bash
flutter pub add get
```

## 使用

**建议在一个独立的`dart`文件中创建所有全局变量的类**

### 创建变量

```dart
import 'package:get/get.dart';
class Controller extends GetxController{
  // 注意在变量的最后添加".obs"用于实时检测变量变化
  var paraX="Hello world!".obs;
}
```

### 创建赋值函数

```dart
import 'package:get/get.dart';
class Controller extends GetxController{
  // 注意在变量的最后添加".obs"用于实时检测变量变化
  var paraX="Hello world!".obs;
  // 注意更新的是变量的"value"，直接给变量赋值无效
  void updateParaX(data) => paraX.value=data;
}
```

### 在Widget中使用

```dart
import 'package:get/get.dart';
// 别忘了导入全局变量的文件
import 'package:para.dart'
// 可以使用StatefulWidget
class myApp extends StatefulWidget{
  // 获取变量
  final Controller c = Get.put(Controller());
  @override
  Widget build(BuildContext context){
    return Center(
      child: Obx(()=>{
        Text(
          // 不需要添加value属性，直接使用
          c.paraX
        )
      })
    )
  }
}
```

### 函数中更新

```dart
import 'package:get/get.dart';
import 'package:para.dart'
class myApp extends StatefulWidget{
  final Controller c = Get.put(Controller());
  @override
  Widget build(BuildContext context){
    return Center(
      child: TextButton(
        onPressed: (){
          // 调用更新函数
          c.updateParaX("Hello, Flutter!")
        },
        child: Text("按钮")
      )
    )
  }
}
```

