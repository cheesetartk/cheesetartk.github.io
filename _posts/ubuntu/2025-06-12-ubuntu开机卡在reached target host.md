---
title: "ubuntu开机卡在reached target host and network name lookups"
tags: ubuntu
---



#### ubuntu开机卡在reached target host and network name lookups

vi /etc/default/grub

将GRUB_CMDLINE_LINUX_DEFAULT=""

修改为GRUB_CMDLINE_LINUX_DEFAULT="text"

update-grub

reboot