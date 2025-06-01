# 📦 PVE Rsync Backup Server 配置说明

## 简介
将 PVE 上挂载的 USB 磁盘，通过 Rsync Daemon 共享给群晖 DSM 使用 Hyper Backup 备份。

---

## 📂 目录结构
- `/mnt/backup-usb`：USB 磁盘挂载目录

---

## 📦 安装 rsync
PVE 默认已自带，可执行以下命令确认：
```bash
rsync --version
```

---

## 📑 配置文件

### /etc/rsyncd.conf
```ini
uid = root
gid = root
use chroot = no
max connections = 4
log file = /var/log/rsyncd.log
pid file = /var/run/rsyncd.pid

[backup-usb]
    path = /mnt/backup-usb
    comment = USB Backup Share
    read only = no
    list = yes
    auth users = default
    secrets file = /etc/rsyncd.secrets
```

### /etc/rsyncd.secrets
```
default:default
```

⚠️ 权限设置：
```bash
chmod 600 /etc/rsyncd.secrets
```

---

## 🖥️ 启动 Rsync Daemon
```bash
rsync --daemon
```

---

## 📶 确认监听端口
默认 873 端口：
```bash
ss -tunlp | grep 873
```

---

## 📌 群晖 Hyper Backup 配置
- 类型：`rsync-compatible server`
- 服务器地址：PVE IP
- 模块名称：`backup-usb`
- 用户名：`default`
- 密码：`default`

测试连接 → 成功

---

## 📜 日志查看
```bash
tail -f /var/log/rsyncd.log
```

---

## 📌 注意事项
- `secrets` 文件权限必须 `600`
- PVE 防火墙需放行 873 端口
- 群晖上 Hyper Backup 仅支持 `rsync-compatible server`，默认不支持 SMB/NFS

---

## ✅ 配置完成
至此，PVE 上 USB 盘可供 DSM Hyper Backup 使用，完美解决 DSM 虚拟机 USB 无法挂载问题。

