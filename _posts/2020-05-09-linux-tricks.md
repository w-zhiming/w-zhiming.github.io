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



## Linux 命令使用

```bash
# ssh key generate.
ssh-keygen -t rsa

# copy key.
ssh-copy-id userb@10.124.84.20

# another way 
scp  ~/.ssh/id_rsa.pub user@host:~/

## host
cat  ~/id_rsa.pub >> ~/.ssh/authorized_keys

# add user
 sudo adduser <username>
# grant user root power.
vim /etc/sudoers   
# root ALL=(ALL)ALL行下添加XXX ALL=(ALL)ALL，XXX为你的用户名。

# change passwd.
passwd username

# userdel 
userdel -r username

##modify file time。
touch -mt  201909052248  test.log
## -m    modify的意思，修改，----更改修改时间
## -t    时间格式【【CC】YYMMddhhmm【.ss】】   CC 代表年前两位，YY代表年后两位，MM月，dd日，hh小时,mm分钟

## set file time to folder.
touch -r 文件  文件夹

```

