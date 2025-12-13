---
title: "rockylinux搭建docker服务"
tags: linux
---



- 关闭防火墙

```
systemctl status firewalld.service    查看防火墙状态
systemctl stop firewalld.service      关闭防火墙
systemctl disable firewalld.service   禁用防火墙
```
- 修改静态IP地址
```
ip addr 查看网卡信息
   
vi /etc/sysconfig/network-scripts/ifcfg-ens33 对应网卡
    
进入文件后执行如下操作:
将BOOTPROTO=DHCP改为static
将ONBOOT=NO改为yes
   
末行添加:
IPADDR=10.24.0.205
NETMASK=255.255.255.0
GATEWAY=10.24.0.1
DNS1=8.8.8.8	
   
按 i 键 进入编辑状态
按 ESC 键,输入 :wq保存退出
   
重启网络
systemctl restart network
 
```
- 更新YUM
```
sudo yum update
sudo yum install yum-utils
```
- 配置Docker YUM阿里源
```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
- 安装Docker
```
yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- 启动配置
```
# 启动Docker
systemctl start docker
 
# 设置开机自启
systemctl enable docker
 
# 不报错就安装成功
docker ps
```
- 镜像加速
```
sudo tee /etc/docker/daemon.json <<EOF
{
	"registry-mirrors": ["https://docker.ricefox.love/"]
}
EOF
```
- 刷新缓存
```
sudo systemctl daemon-reload
sudo systemctl restart docker
```
- 查看Docker版本
```
docker -v
Docker version 27.0.3, build 7d4bcd8
```