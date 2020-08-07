# Docker install vsftpd

## Install vsftpd



```bash
docker run -d \
-v /mydata/ftp/root:/home/vsftpd \
-v /mydata/ftp/log:/var/log/vsftpd \
-v /mydata/ftp/etc:/etc/vsftpd \
-e FTP_USER=Besta -e FTP_PASS=Best@2020 \
-p 8091:21 \
-p 8092-8093:8092-8093 \
-e PASV_MIN_PORT=8092 -e PASV_MAX_PORT=8093 \
--name ftp --restart=always fauria/vsftpd

```

#  Add new user

```bash
## 1. enter bash.
docker exec -i -t vsftpd bash

## 2. create user folder.
mkdir /home/vsftpd/xxx

## 3. edit user config, add user/pwd
vi /etc/vsftpd/virtual_users.txt

## 4. make db.
/usr/bin/db_load -T -t hash -f /etc/vsftpd/virtual_users.txt /etc/vsftpd/virtual_users.db

## 5. restart docker
docker restart vsftpd

```

  