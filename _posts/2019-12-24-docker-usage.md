# Docker usage

## Install

```bash
brew cask install docker
```

## 镜像加速

鉴于国内网络问题，后续拉取 Docker 镜像十分缓慢，我们可以需要配置加速器来解决，我使用的是网易的镜像地址：http://hub-mirror.c.163.com。

在任务栏点击 Docker for mac 应用图标 -> Perferences... -> Daemon -> Registry mirrors。在列表中填写加速器地址即可。修改完成之后，点击 Apply & Restart 按钮，Docker 就会重启并应用配置的镜像地址了。

## Docker 容器使用

```bash

## 获取镜像
docker pull ubuntu
## 启动容器 -i: 交互式操作, -t: 终端。
docker run -it ubuntu /bin/bash

## 查看所有的容器
docker ps -a

## docker start 启动一个已停止的容器：
docker start b750bbbcfd88

## docker 进入容器

docker attach [id] #执行完退出容器

docker exec  -it [id] /bin/bash #执行后不退出

## 导出和导入容器

docker export 1e560fca3906 > ubuntu.tar

## 导入容器快照
cat docker/ubuntu.tar | docker import - test/ubuntu:v1
也可以，例如：

#通过指定 URL 或者某个目录来导入
docker import http://example.com/exampleimage.tgz example/ imagerepo

#删除容器
docker rm -f 1e560fca3906

#web 容器

#运行， -P 随机端口， -p 自定义端口
docker run -d -P training/webapp python app.py
docker run -d -p 5000:5000 training/webapp python app.py

## 查看容器端口
docker port bf08b7f2cd89

##查看LOG
docker logs -f bf08b7f2cd89

##查看WEB应用程序容器的进程
docker top bf08b7f2cd89

#检查 WEB 应用程序
docker inspect bf08b7f2cd89

#更新一个或多个容器的配置
docker update --restart=always abebf7571666
```

## image 使用

```bash

# 获取一个新的镜像
docker pull ubuntu:13.10

# 查找镜像
docker search [image]

# 删除镜像
docker rmi [image]
