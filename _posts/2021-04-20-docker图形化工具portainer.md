> # 吊炸天的 Docker 图形化工具 Portainer
>
> 

- 首先下载Portainer的Docker镜像；

```
docker pull portainer/portainer
```

- 然后再使用如下命令运行Portainer容器；

```
docker run -p 9000:9000 -p 8000:8000 --name portainer \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /mydata/portainer/data:/data \
-d portainer/portainer
```

- 第一次登录的时候需要创建管理员账号，访问地址：http://xxx.xxx.xxx.xxx:9000/

