# Linux常用命令

## 查看IP地址

- IPv4地址

  ```bash
  curl 4.ipw.cn
  ```

- IPv6地址

  ```bash
  curl 6.ipw.cn
  ```


## 安装指定版本的`node.js`

以node.js@14为例：

```bash
sudo curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## nginx

### 安装

1. ```bash
   sudo apt update
   sudo apt upgrade
   ```

2. ```bash
   sudo apt install nginx
   ```

3. ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

4. ```bash
   sudo systemctl status nginx
   ```

## 配置文件

一般位于`/etc/nginx/nginx.conf`

内容大概如下：

```bash
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
}

http {
	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	gzip on;

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
    
    server {
       # 这里是你需要添加的
    }
}
```

### 添加静态页面

**（下面代码仅显示server部分）**

```bash
server{
	listen 80;	# 端口号，一般为80
	server_name example.com;	# 网站名字
	
	ssl on;	# 启动ssl证书（如果有）
  ssl_certificate /path/to/example.com.pem;	# ssl证书位置
  ssl_certificate_key /path/to/example.com.key;	# ssl key的位置
  
  # 访问根目录=>
  location /{
  	root /path/to/folder;	# 静态页面的目录
  	index index.html;	# 主页文件名
  }
}
```

## 反向代理

将某个端口映射到另外一个端口

例如下面的例子就是将8080端口映射到80/api

```bash
server{
	listen 80;	# 端口号，一般为80
	server_name example.com;	# 网站名字
	
	ssl on;	# 启动ssl证书（如果有）
  ssl_certificate /path/to/example.com.pem;	# ssl证书位置
  ssl_certificate_key /path/to/example.com.key;	# ssl key的位置
  
  # 访问根目录=>
  location /{
  	root /path/to/folder;	# 静态页面的目录
  	index index.html;	# 主页文件名
  }
  
  # 反向代理，当访问到/api时=>
  location /api{
  	proxy_pass http://127.0.0.1:8080/api
  }
}
```

⚠️注意：如果反向代理使用的是SpringBoot，将项目中的目录和`nginx`配置匹配：

在`application.properties`文件中添加：

```bash
server.servlet.context-path=/api
```

### 重启nginx

```bash
sudo systemctl restart nginx
```
