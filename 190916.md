# Mongo DB 配置副本集服务

1. 修改主节点的config， 增加 replication服务

   ```
   replication:
   replSetName: "rs0"
   ```

2. 增加副节点配置 rs.cfg.

  ```
    storage:
    dbPath: E:\MongoDB\Server\4.2\data-rs
    journal:
        enabled: true

    #  engine:
    #  mmapv1:
    #  wiredTiger:

    # where to write logging data.
    systemLog:
    destination: file
    logAppend: true
    path:  E:\MongoDB\Server\4.2\log\rs.log

    # network interfaces
    net:
    port: 3003
    # bindIp: 127.0.0.1
    bindIp: 0.0.0.0

    #processManagement:

    #security:

    #operationProfiling:

    replication:
    replSetName: "rs0"
  ```

3. 添加服务
    ```
    sc create MongoDB-RS binpath="\"C:\Program Files\MongoDB\Server\4.2\bin\mongod.exe\" --config \"C:\Program Files\MongoDB\Server\4.2\bin\rs.cfg\" --service"
    ```
4. 连接primary节点， 增加副本集
    ```
    rs.initiate()
    rs.conf()
    rs.add(“f4a.5dkg.net:3003")
    rs.status()
    ```