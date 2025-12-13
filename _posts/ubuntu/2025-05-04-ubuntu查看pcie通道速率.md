---
title: "ubuntu查看pcie通道速率率"
tags: ubuntu
---



Linux系统查看方法‌
‌查看显卡PCIe总线ID‌
执行命令定位显卡设备编号：


lspci | grep -i nvidia  # 适用于NVIDIA显卡
lspci | grep -i amd     # 适用于AMD显卡
输出示例：01:00.0 VGA compatible controller: NVIDIA Corporation GA102 [GeForce RTX 3090]，其中01:00.0为总线ID‌

‌查看当前运行速度和位宽‌
通过以下命令查看实时速率（如PCIe 4.0 x16）：


sudo lspci -vv -s <总线ID> | grep -i "LnkSta"

LnkSta: Speed 8GT/s (PCIe 3.0), Width x16
‌Speed‌: 对应PCIe版本（如8GT/s为PCIe 3.0，16GT/s为PCIe 4.0）‌14
‌Width‌: 当前通道数（如x8、x16）‌23。
‌脚本自动化查询（可选）‌
使用脚本批量提取设备信息：


#!/bin/bash
device_info=$(lspci | grep -i nvidia)
echo "$device_info" | while read -r line; do
  id=$(echo $line | awk '{print $1}')
  sudo lspci -vv -s $id | grep -iE "Width|Speed"
done
可快速获取多显卡的PCIe状态‌







优化liunx/Ubuntu开机卡在等待网络连接a start job is running for wait network

cd /etc/systemd/system/network-online.target.wants/

vi systemd-networkd-wait-online.service

在[Service]栏最后加入如下命令

TimeoutStartSec=2sec

保存重新开机即可搞定