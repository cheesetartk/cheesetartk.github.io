---
title: "ubuntu使用ipmitool操作bmc"
tags: ubuntu
---



更改BMC密码

apt install ipmitool
ipmitool user list 1 #BMC通道,默认1
ipmitool user set password 2 "AD@123456"



更改BMC地址为dhcp

ipmitool lan print 查看当前通道号(默认1)
ipmitool lan set 1 ipsrc dhcp

