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

