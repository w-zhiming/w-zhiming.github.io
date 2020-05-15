# gitlab基本维护和使用

## 基本介绍

GitLab是一个自托管的Git项目仓库，可以自己搭建个人代码管理的仓库，功能与github类似。

## 安装

[下载 gitlab下载地址](https://about.gitlab.com/downloads/)

### 安装依赖的包

```bash
sudo yum install curl-devel
sudo yum install expat-devel
sudo yum install gettext-devel
sudo yum install openssl-devel
sudo yum install zlib-devel
sudo yum install perl-devel
sudo yum install curl
sudo yum install openssh-server
sudo yum install openssh-clients
sudo yum install postfix
sudo yum install cronie
```

Ubuntu系统使用apt-get方式安装依赖包。

### 使用gitlab官网的脚本安装

```bash
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```

### 使用gitlab的yum安装gitlab

```bash
sudo yum install gitlab-ce
```

安装完毕后，使用Web登录

进入gitlab的管理页面，进行常用的分组，工程，用户等功能点的维护。

## gitlab运维操作

### 初次配置服务

```bash
sudo gitlab-ctl reconfigure
```

### 启动服务

```bash
sudo gitlab-ctl start
```

### 停止服务

```bash
sudo gitlab-ctl stop
```

### 重启服务

```bash
sudo gitlab-ctl restart
```

### 修改配置

```bash
vim /etc/gitlab/gitlab.rb
sudo gitlab-ctl  reconfigure
```

### 检查服务的日志信息

```bash 
## 检查redis的日志
sudo gitlab-ctl tail redis

## 检查postgresql的日志
sudo gitlab-ctl tail postgresql

## 检查gitlab-workhorse的日志
sudo gitlab-ctl tail gitlab-workhorse

## 检查logrotate的日志
sudo gitlab-ctl tail logrotate

## 检查nginx的日志
sudo gitlab-ctl tail nginx

##检查sidekiq的日志
sudo gitlab-ctl tail sidekiq

## 检查unicorn的日志
sudo gitlab-ctl tail unicorn
```
　　
### 检查服务状态

```bash
sudo gitlab-ctl status
```

一般服务状态显示信息

显示格式：

状态 ： 进程名称：（进程ID）运行时间（秒）；进程的日志服务进程和运行时间

```bash
run: gitlab-workhorse: (pid 4752) 10759s; run: log: (pid 1077) 13185s
run: logrotate: (pid 12616) 3557s; run: log: (pid 1079) 13185s
run: nginx: (pid 4764) 10758s; run: log: (pid 1076) 13185s
run: postgresql: (pid 4770) 10757s; run: log: (pid 1073) 13185s
run: redis: (pid 4778) 10757s; run: log: (pid 1072) 13185s
run: sidekiq: (pid 4782) 10756s; run: log: (pid 1075) 13185s
run: unicorn: (pid 4786) 10756s; run: log: (pid 1074) 13185s
```

状态   说明

run    运行状态
down   服务停止
常见的问题

```text
## 页面显示500，Whoops， something went wrong on our end.500

Whoops, something went wrong on our end.

Try refreshing the page, or going back and attempting the action again.

Please contact your GitLab administrator if this problem persists.
```

### 如何检查和定位问题

- 使用命令检查所有服务的状态

```bash
sudo gitlab-ctl status
```

检查服务状态如下

```text
run: gitlab-workhorse: (pid 4752) 10862s; run: log: (pid 1077) 13288s
run: logrotate: (pid 16553) 59s; run: log: (pid 1079) 13288s
run: nginx: (pid 4764) 10861s; run: log: (pid 1076) 13288s
run: postgresql: (pid 4770) 10860s; run: log: (pid 1073) 13288s
run: redis: (pid 4778) 10860s; run: log: (pid 1072) 13288s
run: sidekiq: (pid 4782) 10859s; run: log: (pid 1075) 13288s
run: unicorn: (pid 4786) 10859s; run: log: (pid 1074) 13288s
```

- 定位问题

从服务状态信息中显示数据库postgresql的状态是down，即服务停止。
检查数据库postgresql的运行日志，检查出现什么错误？

```bash
$ sudo gitlab-ctl tail postgresql

==> /var/log/gitlab/postgresql/state <==
==> /var/log/gitlab/postgresql/current <==
2017-12-21_02:49:51.42192 FATAL: terminating connection due to administrator command
2017-12-21_02:49:51.42194 FATAL: terminating connection due to administrator command
2017-12-21_02:49:51.42194 LOG: autovacuum launcher shutting down
2017-12-21_02:49:51.42287 FATAL: terminating connection due to administrator command
2017-12-21_02:49:51.42289 FATAL: terminating connection due to administrator command
2017-12-21_02:49:51.42463 LOG: shutting down
2017-12-21_02:49:51.59345 LOG: database system is shut down
2017-12-21_02:50:43.38811 LOG: database system was shut down at 2017-12-21 02:49:51 GMT
2017-12-21_02:50:43.41991 LOG: database system is ready to accept connections
2017-12-21_02:50:43.42055 LOG: autovacuum launcher started
```

日志显示，数据库的访问权限应该是只有用户本身有读写执行的权限，用户组和其他用户不能有权限。
修改数据库数据的权限后，检查服务运行正常。
了解了问题的定位和解决方式，其他问题也很容易在日志中发现和解决，问题可能是磁盘空间少，用户权限错误或者其他原因。

### gitlab管理员密码忘记，怎么重置密码

- root用户下，执行

> ` gitlab-rails console production `

- 获得用户数据，修改用户密码

```bash
[root@svr34 bin]# gitlab-rails console production
Loading production environment (Rails 4.2.5.2)
irb(main):001:0> user = User.where(id: 1).first
=> #<User id: 1, email: "admin@example.com", ...
irb(main):002:0> user.password=12345678
=> 12345678
irb(main):003:0> user.password_confirmation=12345678
=> 12345678
irb(main):004:0> user.save!
=> true
irb(main):005:0> quit
```

***密码没有使用引号，奇怪的是使用单引号或双引号，密码就无效，估计是包含了这个字符，不包含，就没有问题。***
***注意save需要使用后面的感叹号!***

## git 客户端

- windows[下载地址](https://git-scm.com/download/win)
- Linux有关的可以直接yum 安装或者apt-get 安装

```bash
Centos: yum install git
Ubuntu： apt-get install git
```
