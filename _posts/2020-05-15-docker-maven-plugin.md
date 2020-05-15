# 使用Maven插件为SpringBoot应用构建Docker镜像

## Docker Registry 2.0搭建

```bash
docker run -d -p 5000:5000 --restart=always --name registry2 registry:2
```

## 服务器Docker 开启远程API

```bash
vi /usr/lib/systemd/system/docker.service

##old
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
##new
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock
```

## docker 支持 http 上传镜像

```bash
## mac docker desktop 直接修改配置deamon 添加即可， 支持http 方式
echo '{ "insecure-registries":["10.180.2.26:5000"] }' > .docker/daemon.json
```

## 重启docker

```bash
systemctl daemon-reload
systemctl stop docker
systemctl start docker
```

## 开启防火墙的docker 端口

```bash
firewall-cmd --zone=public --add-port=2375/tcp --permanent
firewall-cmd --reload
```

## maven 插件配置

```xml
    <plugin>
        <groupId>com.spotify</groupId>
        <artifactId>docker-maven-plugin</artifactId>
        <version>1.1.0</version>
        <executions>
            <execution>
                <id>build-image</id>
                <phase>package</phase>
                <goals>
                    <goal>build</goal>
                </goals>
            </execution>
        </executions>
        <configuration>
            <imageName>epad/${project.artifactId}:${project.version}</imageName>
            <dockerHost>http://10.180.2.26:2375</dockerHost>
            <baseImage>java:8</baseImage>
            <entryPoint>["java", "-jar","/${project.build.finalName}.jar"]
            </entryPoint>
            <resources>
                <resource>
                    <targetPath>/</targetPath>
                    <directory>${project.build.directory}</directory>
                    <include>${project.build.finalName}.jar</include>
                </resource>
            </resources>
        </configuration>
    </plugin>
```