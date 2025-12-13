---
title: "docker部署memos"
tags: docker
---



```
mkdir /usr/local/share/applications/memos
docker run -d --name memos-a -p 5230:5230 -v /usr/local/share/applications/memos:/var/opt/memos neosmemo/memos:latest
```