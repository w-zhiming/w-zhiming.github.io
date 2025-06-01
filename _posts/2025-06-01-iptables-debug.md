
# 📦【iptables + v2ray 转发调试指南】

## 📌 说明：
本文档用于排查、确认内网设备（如 Xbox）是否通过 iptables 重定向到 v2ray 的代理端口。

---

## 📋 核心操作步骤

### 🎯 查看 iptables 规则命中情况

```bash
iptables -t nat -L PREROUTING -n -v --line-numbers
```

- 查看 `pkts`（命中次数）和 `bytes`（流量字节数）
- 确认目标规则是否递增

---

### v2ray 配透明代理入站
在 v2ray 的 inbounds 加一个透明代理端口，比如 12345：

```json

"inbounds": [
  {
    "port": 12345,
    "protocol": "dokodemo-door",
    "settings": {
      "network": "tcp,udp",
      "followRedirect": true
    },
    "sniffing": {
      "enabled": true,
      "destOverride": ["http", "tls"]
    }
  }
]
```

### 🎯 查看 v2ray 监听端口

```bash
netstat -tunlp | grep 12345
```

应返回类似：

```
tcp        0      0 0.0.0.0:12345           0.0.0.0:*               LISTEN      1234/v2ray
```

---

### 🎯 实时抓包查看流量是否到达

```bash
tcpdump -i br0 port 12345
```

或者针对 Xbox IP 定向抓：

```bash
tcpdump -i br0 src 192.168.1.80 and port 12345
```

---

### 🎯 查看 v2ray 日志记录

如果 v2ray 配置中启用了 log：

```json
"log": {
  "access": "/tmp/opt/var/log/v2ray/access.log",
  "error": "/tmp/opt/var/log/v2ray/error.log",
  "loglevel": "info"
}
```

查看日志：

```bash
tail -f /tmp/opt/var/log/v2ray/access.log
```

---

## 📌 常用 iptables 操作

### 添加 Xbox 转发规则：
③ iptables 转发 Xbox 的流量到 v2ray

```bash
# TCP
iptables -t nat -A PREROUTING -s 192.168.1.80 -p tcp -j REDIRECT --to-ports 12345

# UDP（如果要，前提是内核支持 TPROXY 或 REDIRECT UDP）
iptables -t nat -A PREROUTING -s 192.168.1.80 -p udp -j REDIRECT --to-ports 12345

```

### 删除指定规则（按行号）

查看行号：

```bash
iptables -t nat -L PREROUTING --line-numbers
```

删除：

```bash
iptables -t nat -D PREROUTING <行号>
```

---

## 📌 清空规则风险提示

### 清空所有规则：

```bash
iptables -F
iptables -t nat -F
```

⚠️ **风险：会删除所有现有转发规则，影响现有代理、端口映射，慎用。**

---

## 📦 v2ray 路由配置排除局域网直连示例

```json
"routing": {
  "rules": [
    {
      "type": "field",
      "ip": [
        "geoip:private"
      ],
      "outboundTag": "direct"
    },
    {
      "type": "field",
      "domain": [
        "geosite:cn"
      ],
      "outboundTag": "direct"
    },
    {
      "type": "field",
      "ip": [
        "0.0.0.0/0"
      ],
      "outboundTag": "proxy"
    }
  ]
}
```

---

## 📋 总结

✅ iptables 命中数确认  
✅ netstat 查看端口监听  
✅ tcpdump 实时抓包  
✅ v2ray 日志追踪  
✅ 路由规则科学配置
