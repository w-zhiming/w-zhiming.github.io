# Linux tricks

## Change linux time zone

```bash
## select time zone.
tzselect -select a time zone
## edit profile, add current timezone.
vim /etc/profile

# time
TZ='Asia/Shanghai'
export TZ

```

## scp copy file without password.

```bash
## way 1, use ssh key.
## way 2, use sshpass.

sshpass -p xxx scp a.txt xxx@192.168.1.101:/home/xxx/a.txt  

```



## 查看端口是否被占用
```bash
lsof -i tcp:port
## (port替换成端口号，比如6379）可以查看该端口被什么程序占用，并显示PID，方便KILL（kill pid）
```


