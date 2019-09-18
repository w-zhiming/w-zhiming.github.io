---
title:  "pm2 & service 配置"
date:   2018-03-31 02:36:26 +0800
tags:   nodejs
---

## pm2 安装
```
npm install -g pm2
```
## pm2 常用命令

假设你现在已经写好了一个app.js的文件，需要启动，你可以使用pm2进行管理

- 启动
```
# pm2 start app.js
# pm2 start app.js --name my-api   #my-api为PM2进程名称
# pm2 start app.js -i 0           #根据CPU核数启动进程个数
# pm2 start app.js --watch   #实时监控app.js的方式启动，当app.js文件有变动时，pm2会自动reload
```
- 查看进程
```
# pm2 list
# pm2 show 0 或者 # pm2 info 0  #查看进程详细信息，0为PM2进程id
```
- 监控
```
# pm2 monit
```
- 停止
```
# pm2 stop all  #停止PM2列表中所有的进程
# pm2 stop 0    #停止PM2列表中进程为0的进程
```
- 重载
```
# pm2 reload all    #重载PM2列表中所有的进程
# pm2 reload 0     #重载PM2列表中进程为0的进程
```
- 重启
```
# pm2 restart all     #重启PM2列表中所有的进程
# pm2 restart 0      #重启PM2列表中进程为0的进程
```
- 删除PM2进程
```
# pm2 delete 0     #删除PM2列表中进程为0的进程
# pm2 delete all   #删除PM2列表中所有的进程
```
- 日志操作
```
# pm2 logs [--raw]   #Display all processes logs in streaming
# pm2 flush              #Empty all log file
# pm2 reloadLogs    #Reload all logs
```
- 升级PM2
```
# npm install pm2@lastest -g   #安装最新的PM2版本
# pm2 updatePM2                    #升级pm2
```
- 更多命令参数请查看帮助
```
# pm2 --help
```

## 配置pm2为服务

- 安装并配置pm2-windows-service
```
npm i -g pm2-windows-service
```
- 添加.pm2的系统环境变量
```
PM2_HOME=C:\Users\zhtop.pm2(路径默认在当前用户下的.pm2)
```
- 以管理员权限打开新的cmd命令行窗口,执行以下命令来安装服务
```
pm2-service-install
```
提示Perform environment setup ? 选 n, 继续,此时, PM2服务已安装成功并已启动, 可以通过 [win + r] - [services.msc] 来查看，服务名称为PM2

- 运行程序
```
pm2 start app.js -n MongoDBserve
pm2 save
```
(pm2 save 很重要, 它保存当前pm2 正在管理的NodeJS服务, 并在开机后恢复这些服务，保存路径为系统环境变量设置的PM2_HOME路径。)