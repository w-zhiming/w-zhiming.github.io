# Mongo replicate set mode authority

## Make key file

```bash
openssl rand -base64 741 >key
```

## Add key file to database

- By config file, such as mongo.cfg, rs.cfg.

```yml
security:
  keyFile: E:\MongoDB\Server\4.2\conf\key
  #authorization: enabled  //注释掉auth
```

- By command line

```bash
docker run --name mongo-primary -v ~/docker/mongo/primary/data:/data/db -v ~/docker/mongo/conf:/opt/keyfile -p 27017:27017 -d mongo --keyFile /opt/keyfile/keyfile --replSet "rs"
docker run --name mongo-second -v ~/docker/mongo/second/data:/data/db -v ~/docker/mongo/conf:/opt/keyfile  -p 27018:27017 -d mongo --keyFile /opt/keyfile/keyfile  --replSet "rs"
```

## Create root user, by shell or other ways

```js
Use admin
db.createUser({ user: 'root', pwd: 'Besta2020', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
```

## Add auth config, Restart

- By config file, open authorization，set enabled，restart.
- By command line, add --auth

## Connect mongo by root user

```Bash
mongo --port 3002 -u root -p Besta2020
```

## Add user for special collection

```javascript
use f4a191118
db.createUser({ user:"f4a", pwd:"Besta2020", roles: [ { role: "dbOwner", db: "f4a191118" } ] });
```

## 连接测试

```javascript
    “mongodb://f4a:Besta2020@f4a.5dkg.net:3002/f4a191118”
```
