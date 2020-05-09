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
