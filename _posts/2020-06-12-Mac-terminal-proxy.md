# MAC下设置Iterm2代理进行加速

## 設置方法：

```bash
alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
alias unsetproxy="unset ALL_PROXY"
```

## 測試方法

```bash
curl ip.cn

curl cip.cc
```

