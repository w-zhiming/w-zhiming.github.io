# 解决LINUX(CENTOS)下SSH连接超时自动断开的问题

- 查看配置

```bash
# 切换SSH目录
# cd /etc/ssh

# 查看sshd_config中关于客户端活动状态的配置
# grep ClientAlive sshd_config
# 默认配置如下
#ClientAliveInterval 0
#ClientAliveCountMax 3

#ClientAliveInterval指定了服务器端向客户端请求消息的时间间隔, 默认是0, 不发送。设置60表示每分钟发送一次, 然后客户端响应, 这样就保持长连接了。
#ClientAliveCountMax表示服务器发出请求后客户端没有响应的次数达到一定值, 就自动断开。正常情况下, 客户端不会不响应，这里设置为5即可。
```

- 备份修改配置

```bash
# cp sshd_config sshd_config.bak

# 启用客户端活动检查，每60秒检查一次，5次不活动断开连接
# sed -i "s/#ClientAliveInterval 0/ClientAliveInterval 60/g" sshd_config
# sed -i "s/#ClientAliveCountMax 3/ClientAliveCountMax 5/g" sshd_config

# 重新加载ssd配置，让配置生效
# service sshd restart

# 查看修改
# grep ClientAlive sshd_config
```

好了，妈妈再也不用担心我的SSH自动断开了。
