
# CentOS7 yum 安装redis

## 安装redis

1. 检查是否有yum源
`yum install redis`
2. 下载fedora的epel仓库
`yum install epel-release`
3. 安装redis数据库
`yum install redis`
4. 安装完毕后，使用下面的命令启动redis服务

    ```bash

        # 启动redis
        service redis start
        # 停止redis
        service redis stop
        # 查看redis运行状态
        service redis status
        # 查看redis进程
        ps -ef | grep redis
    ```

5. 设置redis为开机自动启动
`chkconfig redis on`

6. 进入redis服务
  
    ```bash
    # 进入本机redis
    redis-cli
    # 列出所有key
    keys *
    ```

## 配置redis

1. 打开配置文件
`vi /etc/redis.conf`
2. 修改默认端口， 查找port 6379 修改
3. 修改默认密码，查找 requirepass foobared
4. 使用配置文件启动 redis
`redis-server /etc/redis.conf`
5. 使用端口登陆
`redis-cli -h 127.0.0.1 -p 6179`
6. 配置redis远程连接
    - bind 127.0.0.1改为 #bind 127.0.0.1 (注释掉)
    - protected-mode yes 改为 protected-mode no
