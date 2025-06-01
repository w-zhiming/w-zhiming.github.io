# PVE (Proxmox VE) 常用命令速查表

## 📦 基础管理

### 查看信息

```bash
pveversion                    # 查看PVE版本
pvesh get /nodes              # 查看集群节点
pvesh get /nodes/{nodename}/status  # 查看节点状态
qm list                       # 虚拟机列表
pct list                      # LXC容器列表
```

### 虚拟机管理 (qm)

```bash
qm create 100 --name testvm --memory 2048 --net0 virtio,bridge=vmbr0  # 创建虚拟机

qm start 100                   # 启动虚拟机
qm stop 100                    # 强制停止
qm shutdown 100                # 软关机
qm destroy 100                 # 删除虚拟机
qm config 100                  # 查看虚拟机配置

qm set 100 --memory 4096       # 修改内存
qm set 100 --cores 4           # 修改CPU核心
qm set 100 --net0 virtio,bridge=vmbr0  # 配置网卡

qm status 100                  # 查看状态
qm monitor 100                 # 进入监控台
```

## 📦 存储管理

```bash
pvesm status                   # 存储池状态
pvesm list local               # 查看local存储内容
pvesm set local --maxfiles 3   # 设置最大备份数
```

## 📦 备份与恢复

```bash
vzdump 100 --mode stop --compress lzo --storage local        # 停机备份
vzdump 100 --mode snapshot --compress lzo --storage local    # 快照备份

qmrestore /var/lib/vz/dump/vzdump-qemu-100-xxx.vma.lzo 100 --unique  # 恢复
```

## 📑 配置文件

```bash
cat /etc/pve/qemu-server/100.conf   # 查看虚拟机配置
nano /etc/pve/qemu-server/100.conf  # 编辑虚拟机配置
```

## 📶 网络管理

```bash
cat /etc/network/interfaces         # 查看/编辑网络
ifup vmbr0                          # 启动网桥
ifdown vmbr0                        # 停止网桥
systemctl restart networking        # 重启网络服务
```

## 📡 硬盘直通

```bash
qm set 100 -sata0 /dev/disk/by-id/xxx,discard=on,ssd=1  # 直通
qm set 100 -delete sata0                                # 删除直通
```

## 🛑 服务管理

```bash
systemctl status pvedaemon.service
systemctl restart pvedaemon.service
systemctl restart pveproxy.service
systemctl restart pvestatd.service
```

## 📖 镜像目录

```bash
/var/lib/vz/template/iso      # ISO目录
/var/lib/vz/template/cache    # LXC目录
```

## 📌 常用技巧

```bash
systemctl list-units | grep pve              # 查看所有PVE服务状态
journalctl -f | grep 100                     # 实时查看某虚拟机日志
qm list | awk '{print $1}' | xargs -I {} qm config {} | grep -i disk  # 查看磁盘占用
```

---

✅ 随时扩展、定制你自己的PVE速查表！
