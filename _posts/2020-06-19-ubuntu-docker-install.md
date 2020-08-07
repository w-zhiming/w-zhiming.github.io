# Ubuntu18.04安装Docker

## 1. 从Ubuntu的仓库直接下载

安装比较简单，这种安装的Docker不是最新版本

```bash
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
```



## 2. 从Docker仓库下载安装

这种安装方式首先要保证Ubuntu服务器能够访问Docker仓库地址：https://download.docker.com/linux/ubuntu，如果能够访问，按照下面的操作步骤进行安装。

```bash
## 查看ubuntu版本
cat /etc/lsb-release
## remove old version
sudo apt-get remove docker docker-engine docker-ce docker.io


sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
## 在/etc/apt/sources.list.d/docker.list文件中添加下面内容
deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable
## 添加秘钥
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
## 安装docker-ce
sudo apt install docker-ce
## version
docker --version
## run hello
docker run hello-world

```



