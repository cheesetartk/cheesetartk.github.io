---
title: "linux更改ip后原ip依然可用的解决方法"
tags: linux
---



因为网络接口在更改IP地址时保留了对原来IP地址的配置信息。
如果你使用ip命令更改了IP地址：

```
sudo ip addr add 192.168.1.100/24 dev ens160
```

然后你可以通过以下命令查看配置：

```
ip addr show ens160
```

接口列出了两个IP地址（一个新地址和一个旧地址）。
要使原来的IP地址不可用，你需要删除旧的IP配置
```
sudo ip addr del 192.168.1.5/24 dev ens160
```