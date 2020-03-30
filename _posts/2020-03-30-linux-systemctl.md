# linux中systemctl详细理解及常用命令

## systemctl理解

Linux 服务管理两种方式service和systemctl
systemd是Linux系统最新的初始化系统(init),作用是提高系统的启动速度，尽可能启动较少的进程，尽可能更多进程并发启动。
systemd对应的进程管理命令是systemctl

### systemctl命令兼容了service

systemctl也会去/etc/init.d目录下，查看，执行相关程序

```bash
    systemctl redis start
    systemctl redis stop
    # 开机自启动
    systemctl enable redis
```

### systemctl命令管理systemd的资源Unit

systemd的Unit放在目录

- /usr/lib/systemd/system(Centos)
- /etc/systemd/system(Ubuntu)

### unit主要有四种类型文件.mount,.service,.target,.wants

- .mount文件
.mount文件定义了一个挂载点，[Mount]节点里配置了What,Where,Type三个数据项

- service文件
.service文件定义了一个服务，分为[Unit]，[Service]，[Install]三个小节

[Unit]
Description:描述，
After：在network.target,auditd.service启动后才启动
ConditionPathExists: 执行条件

[Service]
EnvironmentFile:变量所在文件
ExecStart: 执行启动脚本
Restart: fail时重启

[Install]
Alias:服务别名
WangtedBy: 多用户模式下需要的

- .target文件
.target定义了一些基础的组件，供.service文件调用

- .wants文件
.wants文件定义了要执行的文件集合，每次执行，.wants文件夹里面的文件都会执行

## 服务常用指令

```bash
    ##启动服务
    systemctl start nginx.service
    ##设置开机启动
    systemctl enable nginx.service
    ##停止开机启动
    systemctl disable nginx.service
    ##查看服务状态
    systemctl status nginx.service
    ##重启服务
    systemctl restart nginx.service
    ##查看所有已启动的服务
    systemctl list-units --type=service
```
