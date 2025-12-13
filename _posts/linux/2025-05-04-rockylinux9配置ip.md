---
title: "rockylinux9配置ip"
tags: linux
---



1. 编辑配置文件

```
cd /etc/NetworkManager/system-connections/
ll
vim 配置文件
```


2. 内容如下：

```
[connection]
id=ens192
uuid=14d47b8e-b926-4fa9-b962-f057bc015d8b
type=ethernet
interface-name=ens192
timestamp=1681721746

[ethernet]

[ipv4]
address1=10.42.40.45/24,10.42.40.1
dns=10.42.40.1;
method=auto

[ipv6]
addr-gen-mode=default
method=auto

[proxy]
```

3. 重启生效：reboot重启
```
#先断开网卡，再次连接网卡，也可使IP配置生效。
nmcli connection down ens192	
nmcli device
nmcli connection up ens192
nmcli device
```