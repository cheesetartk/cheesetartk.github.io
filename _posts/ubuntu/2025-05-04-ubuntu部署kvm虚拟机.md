---
title: "ubuntu部署kvm虚拟机"
tags: ubuntu
---



更新软件包

sudo apt upgrade -y

安装必要包

sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager

查看状态

systemctl is-active libvirtd

lsmod | grep kvm

systemctl start libvirtd

systemctl enabled libvirtd

systemctl status libvirtd

安装网桥

sudo apt install bridge-utils

配置网桥

gedit /etc/netplan/01-network-manager-all.yaml

network:
  version: 2
  #renderer: NetworkManager
  ethernets:
        ens33:(网卡名称)
            dhcp4: false
            dhcp6: false
  bridges:
        br0:
            addresses: [192.168.159.133/24]（本机IP）
            gateway4: 192.168.159.1（网关）
            nameservers:
                addresses: [192.168.159.2, 114.114.114.114]（DNS）
                search: [msnode]
            interfaces: [ens33]（网卡名称）

sudo netplan apply

mkdir /etc/qemu

vi /etc/qemu/bridge.conf

allow br0 (这里的br0跟之前创建的虚拟网桥相同)
allow all

sudo chmod 777 /etc/qemu/bridge.conf

sudo chmod 4755 /usr/lib/qemu/qemu-bridge-helper

创建虚拟机

virt-install -n Ubuntu20_VM0 -r 2048 --vcpus=2 --os-variant=ubuntu20.04 --accelerate -c /home/ubuntu/fnos-0824.iso --disk path=/home/ubuntu/fnos-0824.img,format=qcow2,bus=virtio,size=20 --network bridge=br0 --vnc --vncport=5996 --vnclisten=0.0.0.0

打开图形化

virt-manager

