# 关闭linux 的swap分区

## 1. 关闭swap分区

```bash
swapoff -a
```



## 2. 修改配置文件 

```bash
vim /etc/fstab
## 删除swap相关行 /mnt/swap swap swap defaults 0 0 这一行或者注释掉这一行

##确认swap已经关闭
free -m

```


