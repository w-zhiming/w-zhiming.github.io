# ElasticsSearch

## 介绍

Elasticsearch 是一个分布式、可扩展、实时的搜索与数据分析引擎。 它能从项目一开始就赋予你的数据以搜索、分析和探索的能力，可用于实现全文搜索和实时数据统计。

## 下载安装elasticsearch

```bash
    #下载
    docker pull elasticsearch:6.4.0
    #修改虚拟内存区域大小，否则会因为过小而无法启动:
    sysctl -w vm.max_map_count=262144
    #使用docker命令启动：
    docker run -p 9200:9200 -p 9300:9300 --name elasticsearch \
    -e "discovery.type=single-node" \
    -e "cluster.name=elasticsearch" \
    -v /mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins \
    -v /mydata/elasticsearch/data:/usr/share/elasticsearch/data \
    -d elasticsearch:6.4.0
    #启动时会发现/usr/share/elasticsearch/data目录没有访问权限，只需要修改/mydata/elasticsearch/data目录的权限，再重新启动。
    chmod 777 /mydata/elasticsearch/data/
    #安装中文分词器IKAnalyzer，并重新启动：
    docker exec -it elasticsearch /bin/bash
    #此命令需要在容器中运行
    elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.4.0/elasticsearch-analysis-ik-6.4.0.zip

    docker restart elasticsearch
```

## 下载安装kibana

```bash

# 下载kibana6.4.0的docker镜像
docker pull kibana:6.4.0

#使用docker命令启动：
docker run --name kibana -p 5601:5601 \
--link elasticsearch:es \
-e "elasticsearch.hosts=http://es:9200" \
-d kibana:6.4.0

#开启防火墙：
firewall-cmd --zone=public --add-port=5601/tcp --permanent
firewall-cmd --reload

#访问地址进行测试：http://192.168.3.101:5601
```
