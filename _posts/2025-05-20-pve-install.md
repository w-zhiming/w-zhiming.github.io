# 
# 📄 PVE 安装与虚拟机管理操作手册

## 📌 Proxmox VE 安装

1. 下载最新版 Proxmox VE ISO：  
   https://www.proxmox.com/en/downloads

2. 制作启动 U 盘（推荐使用 balenaEtcher / Rufus）

3. 启动目标机器，选择从 U 盘启动

4. 安装 PVE（默认配置安装即可）

## 📌 登录 PVE 管理后台

浏览器访问 `https://<PVE服务器IP>:8006`

## 📌 上传 ISO 镜像

1. 在 PVE 管理后台 → `存储(local)` → `ISO 镜像` → `上传`
2. 选择你的系统镜像上传

## 📌 PVE 虚拟机创建流程

### 1️⃣ 新建虚拟机  

```bash
qm create 100 --name myvm --memory 4096 --cores 2 --net0 virtio,bridge=vmbr0
```

### 2️⃣ 添加系统盘  

```bash
qm set 100 --cdrom local:iso/dsm7.2.iso
```

或直通硬盘：

```bash
qm set 100 --sata0 /dev/disk/by-id/ata-WDC_WD30EZRZ-00Z5HB0,size=2930266584K
```

### 3️⃣ 配置硬盘  

```bash
qm set 100 --scsi0 local-lvm:32
```

或直通 SATA/SSD：

```bash
qm set 100 --sata1 /dev/disk/by-id/ata-CT240BX500SSD1_1919E1803A5D,discard=on,ssd=1
```

### 4️⃣ 设置网卡桥接  

```bash
qm set 100 --net0 e1000,bridge=vmbr0
```

## 📌 启动虚拟机  

```bash
qm start 100
```

## 📌 停止虚拟机  

```bash
qm stop 100
```

## 📌 删除虚拟机  

```bash
qm destroy 100
```

## 📌 虚拟机备份  

```bash
vzdump 100 --mode stop --storage local --compress lzo
```

## 📌 导入现成镜像作为硬盘  

```bash
qm create 101 --name dsm --memory 4096 --cores 2 --net0 virtio,bridge=vmbr0
qm importdisk 101 dsm72.qcow2 local-lvm
qm set 101 --scsi0 local-lvm:vm-101-disk-0
qm set 101 --boot order=scsi0
```

## 📌 查看 PVE 磁盘设备 ID  

```bash
ls -l /dev/disk/by-id/
```

## 📌 查看虚拟机配置文件  

```bash
cat /etc/pve/qemu-server/100.conf
```

## 📌 编辑虚拟机配置  

```bash
cp /etc/pve/qemu-server/100.conf /etc/pve/qemu-server/100.conf.bak
nano /etc/pve/qemu-server/100.conf
```

## 📌 直通 USB 设备  

```bash
lsusb
qm set 100 --usb0 host=174c:55aa,usb3=1
```

---

✅ 完整项目清单还能继续追加：群晖直通、V2Fly Docker 配置、ContainerManager 镜像加速方案、Proxmox VE 磁盘调优、快照与还原方法。
