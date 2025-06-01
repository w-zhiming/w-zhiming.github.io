# container-manager config

1. 群晖网络设置-代理服务器 设置科学上网。

2. 编辑 /var/packages/ContainerManager/etc/dockerd.json， 增加proxies， 科学上网
```json
{
    "data-root": "/var/packages/ContainerManager/var/docker",
    "log-driver": "db",
    "proxies": {
        "http-proxy": "127.0.0.1:1087",
        "https-proxy": "127.0.0.1:1087"
    },
    "registry-mirrors": [
        "https://rx59rk07.mirror.aliyuncs.com",
        "https://dockerhub.azk8s.cn",
        "https://hub-mirror.c.163.com",
        "https://mirror.ccs.tencentyun.com",
        "https://docker.m.daocloud.io",
        "https://docker.jianmuhub.com",
        "https://huecker.io",
        "https://dockerhub.timeweb.cloud",
        "https://dockerhub1.beget.com",
        "https://noohub.ru"
    ],
    "seccomp-profile": "unconfined",
    "storage-driver": "aufs"
}
```

1. run v2fly/core
2. mv
``` bash 
  docker run -d --name v2ray \
  --restart=always \
  -v /volume1/docker/v2ray/config:/etc/v2ray \
  -v /volume1/docker/v2ray/log:/var/log/v2ray \
  --network=host \
  v2fly/v2fly-core run -c /etc/v2ray/config.json
```