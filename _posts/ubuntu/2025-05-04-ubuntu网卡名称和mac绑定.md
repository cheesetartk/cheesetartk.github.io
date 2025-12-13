---
title: "ubuntu网卡名称和mac绑定"
tags: ubuntu
---

sudo -i echo 'SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="01:23:45:67:89:ab", ATTR{dev_id}=="0x0", ATTR{type}=="1", KERNEL=="e*", NAME="eth0"' >> /etc/udev/rules.d/70-persistent-net.rules