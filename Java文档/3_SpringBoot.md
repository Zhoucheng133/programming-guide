# SpringBoot

## 创建一个SpringBoot项目

可以通过这个链接在线创建：[点击这里查看](https://start.spring.io/)

### 项目配置

添加的依赖：

- SpringBoot DevTools：开发者工具
- LomBok：转发Java中的类参数（传递到前端以对象的形式）
- Spring Web：可以使用注解`@RequestMapping`

### 为打包做准备

在最后添加：

```xml
<build>
		<plugins>
			<plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
		</plugins>
	</build>
```

这个依赖可以导出`jar`包

### 修改端口号

在目录`src/main/java/xxx/resources/application.properties`中添加：

```properties
server.port=1234
```

### 修改访问目录

同样在目录`src/main/java/xxx/resources/application.properties`中添加：

```properties
server.servlet.context-path=/api
```

