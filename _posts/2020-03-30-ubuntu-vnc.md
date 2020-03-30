# Ubuntu16.04 安装 x11vnc 远程桌面并设置开机自动启动

## 安装x11vnc

```bash
    sudo apt-get install x11vnc
```

## 设置连接密码

```bash
    ## 默认保存在当前用户的.vnc 目录
    sudo x11vnc -storepasswd
    ## 保存到系统etc下使用如下方式
    sudo x11vnc -storepasswd in /etc/x11vnc.pass
```

## 新建服务文件

```bash
    ## 注意目录是systemd/system目录
    sudo vi /lib/systemd/system/x11vnc.service
```

## x11vnc.service 内容

```conf

[Unit]
Description=Start x11vnc at startup.
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/bin/x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /home/<USERNAME>/.vnc/passwd -rfbport 5900 -shared

[Install]
WantedBy=multi-user.target

```

## 设置开机自启服务

```bash
sudo systemctl daemon-reload
sudo systemctl enable x11vnc.service
sudo systemctl start x11vnc.service
```
