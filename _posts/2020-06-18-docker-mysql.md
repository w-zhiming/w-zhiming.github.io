# Setup mysql in docker

```bash
# download mysql lastest.
docker pull myql

# copy mysql config.
docker cp 776427d54b17:/etc/mysql/. /mydata/mysql/conf

#run mysql
docker run -p 3306:3306 --name mysql \

-v /mydata/mysql/log:/var/log/mysql \

-v /mydata/mysql/data:/var/lib/mysql \

-v /mydata/mysql/conf:/etc/mysql \

-e MYSQL_ROOT_PASSWORD=A1b2c3d4 \

-d mysql

## login mysql container.
docker exec -it mysql "/bin/bash"

## open remote access.
use mysql
update user set host = '%' where user = 'root';
flush privileges;

## mysql8.0 use caching_sha2_password, so old tools can't login, we need change to  native password.
ALTER USER 'root' IDENTIFIED WITH mysql_native_password BY 'A1b2c3d4';

```

