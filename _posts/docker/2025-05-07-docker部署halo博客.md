---
title: "docker部署halo博客"
tags: docker
---



安装wget
```
yum clean all  清除缓存
yum makecache  将yum 源加载到缓存
yum install wget  安装命令
```

安装halo
```
创建 工作目录
mkdir /usr/local/share/applications/halo && cd /usr/local/share/applications/halo

下载示例配置文件到 工作目录
wget https://dl.halo.run/config/application-template.yaml -O ./application.yaml

拉取 Halo 镜像
docker pull halohub/halo:1.6

创建容器
docker run -it -d --name halo-a -p 8090:8090 -v /usr/local/share/applications/halo:/root/.halo --restart=unless-stopped halohub/halo:1.6
```

编辑配置文件(可选)
```
vim application.yaml

spring:
  datasource:
    driver-class-name: org.h2.Driver
    url: jdbc:h2:file:~/.halo/db/halo
    username: admin
    password: 123456
  h2:
    console:
      settings:
        web-allow-others: false 改为true开启web管理页面
      path: /h2-console
      enabled: false 改为true开启web管理页面
```

版本：1.6.1
数据库：H2 1.4.199 (2019-03-13)
运行模式：production