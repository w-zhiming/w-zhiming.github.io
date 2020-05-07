# Update Centos 7 Repo

```bash

## show current repo.
cd /etc/yum.repos.d && ls

## backup old repo.
mkdir repo_bak && mv *.repo repo_bak/

## scratch repo file
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
wget http://mirrors.aliyun.com/repo/Centos-7.repo

## clean & make cache.
yum clean all && yum makecache

## scrath epel(extra package about enterprice linux) repo.
yum list |grep epel-release
yum install -y epel-release
wget -O /etc/yum.repos.d/epel-7.repo
wget -O /etc/yum.repos.d/epel-7.repo http://mirrors.aliyun.com/repo/epel-7.repo

## clean cache again, then check repo, done!
yum clean all
yum makecache
yum repolist enabled
yum repolist all
```
