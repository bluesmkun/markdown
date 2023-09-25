# Docker安装Nginx Proxy Manager
## Nginx proxy manager是一个很简单的反向代理工具。
官网：https://nginxproxymanager.com

### 门槛极低，操作简单，不需要你掌握很复杂的Nginx配置知识，只需要几步就能很轻松完成反向代理的设置和SSL证书的部署

### 开始部署
服务器环境：Debian 10（Ubuntu 20.04也可以）或以上版本

### 升级 packages
```
apt install wget curl sudo vim git -y
```
### 安装 Docker 环境
```
wget -qO- get.docker.com | bash
```

```
systemctl enable docker  # 设置开机自动启动
```

### 安装 Docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
### 安装 Nginx Proxy Manager
#### 创建安装目录
```
mkdir -p /root/data/docker_data/npm
```

```
cd /root/data/docker_data/npm
```

#### 这边我们直接用 docker 的方式安装。

```
vim docker-compose.yml
```

#### 输入法下，按 i

```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'  # 冒号左边可以改成自己服务器未被占用的端口
      - '81:81'  # 冒号左边可以改成自己服务器未被占用的端口
      - '443:443' # 冒号左边可以改成自己服务器未被占用的端口
    volumes:
      - ./data:/data # 冒号左边可以改路径，现在是表示把数据存放在在当前文件夹下的 data 文件夹中
      - ./letsencrypt:/etc/letsencrypt  # 冒号左边可以改路径，现在是表示把数据存放在在当前文件夹下的 letsencrypt 文件夹中
```
#### 按一下 esc，然后 :wq 保存退出，之后

### 运行并访问 Nginx Proxy Manager
```
cd /root/data/docker_data/npm   # 来到 dockercompose 文件所在的文件夹下
```

```
docker-compose up -d
```
### 理论上我们就可以输入 http://ip:81 访问了。
### 默认登陆名和密码：

```
Email:    admin@example.com
Password: changeme
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MjkzMTU5NzVdfQ==
-->