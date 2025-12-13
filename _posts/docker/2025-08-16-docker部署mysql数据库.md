---
title: "docker部署mysql"
tags: docker
---



拉取镜像

```
docker pull mysql:8.4.1
```
创建 工作目录
```
mkdir -p /home/apps/mysql8.4.1
chmod 777 -R /home/apps/mysql8.4.1
cd /home/apps/mysql8.4.1
```
运行容器

```
docker run -d --restart=unless-stopped \
--name mysql8.4.1 -p 3306:3306 \
--privileged=true \
-v /home/apps/mysql8.4:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123234 \
-e MYSQLD_DEFAULT_AUTHENTICATION_PLUGIN=mysql_native_password \
-e TZ=Asia/Shanghai mysql:8.4.1 \
--character-set-server=utf8mb4 \
--collation-server=utf8mb4_general_ci
```

远程访问配置

```
docker exec -it mysql8.4.1 mysql -uroot -p
ALTER USER 'root'@'%' IDENTIFIED BY '123234';
FLUSH PRIVILEGES;
```

创建远程用户

```
CREATE USER '用户名'@'%' IDENTIFIED BY '密码';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
```

