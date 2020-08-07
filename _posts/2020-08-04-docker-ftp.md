# Docker install ELK

## Download images



```bash
docker pull elasticsearch:6.4.0
docker pull logstash:6.4.0
docker pull kibana:6.4.0

```

#  Elasticsearch setting

```bash
elasticsearch
需要设置系统内核参数，否则会因为内存不足无法启动。

# 改变设置
sysctl -w vm.max_map_count=262144

# 使之立即生效
sysctl -p
# 需要创建/mydata/elasticsearch/data目录并设置权限，否则会无权限访问而启动失败。

# 创建目录
mkdir /mydata/elasticsearch/data/

# 创建并改变该目录权限
chmod 777 /mydata/elasticsearch/data

```

  

# Logstash config

```properties
input {
  tcp {
    mode => "server"
    host => "0.0.0.0"
    port => 4560
    codec => json_lines
  }
}
output {
  elasticsearch {
    hosts => "es:9200"
    index => "epad-logstash-%{+YYYY.MM.dd}"
  }
}
```



docker-compose.yml

```yaml
version: '3'
services:
  elasticsearch:
    image: elasticsearch:6.4.0
    container_name: elasticsearch
    environment:
      - "cluster.name=elasticsearch" #设置集群名称为elasticsearch
      - "discovery.type=single-node" #以单一节点模式启动
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m" #设置使用jvm内存大小
    volumes:
      - /mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins #插件文件挂载
      - /mydata/elasticsearch/data:/usr/share/elasticsearch/data #数据文件挂载
    ports:
      - 9200:9200
      - 9300:9300
  kibana:
    image: kibana:6.4.0
    container_name: kibana
    links:
      - elasticsearch:es #可以用es这个域名访问elasticsearch服务
    depends_on:
      - elasticsearch #kibana在elasticsearch启动之后再启动
    environment:
      - "elasticsearch.hosts=http://es:9200" #设置访问elasticsearch的地址
    ports:
      - 5601:5601
  logstash:
    image: logstash:6.4.0
    container_name: logstash
    volumes:
      - /mydata/logstash/logstash-springboot.conf:/usr/share/logstash/pipeline/logstash.conf #挂载logstash的配置文件
    depends_on:
      - elasticsearch #kibana在elasticsearch启动之后再启动
    links:
      - elasticsearch:es #可以用es这个域名访问elasticsearch服务
    ports:
      - 4560:4560
```



# docker-compose install

```bash
## download
curl -L https://get.daocloud.io/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

## 修改该文件的权限为可执行
chmod +x /usr/local/bin/docker-compose

## 查看是否已经安装成功
docker-compose --version

## run 
docker-compose up -d

```



# config spring boot logback.xml

```bash
## application.yml

logging:
  config: classpath:logback-spring.xml
  level:
    com.besta.elderpad: debug

## logback add el

<!--    输出到logstash的appender-->
    <appender name="LOGSTASH" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
        <destination>localhost:4560</destination>
        <encoder charset="UTF-8" class="net.logstash.logback.encoder.LogstashEncoder"/>
    </appender>
    <root level="INFO">
        <appender-ref ref="CONSOLE"/>
        <appender-ref ref="FILE"/>
        <appender-ref ref="LOGSTASH"/>
    </root>

```

