---
title: "docker修改mysql配置"
tags: docker
---



docker cp 容器id:/etc/my.cnf ../home 将docker中文件复制到宿主机进行编辑
docker cp ../home/my.cnf 容器id:/etc/ 将编辑后的文件覆盖回去