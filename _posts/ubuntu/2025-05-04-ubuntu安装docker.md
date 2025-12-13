---
title: "ubuntu安装docker"
tags: ubuntu
---



更换清华源：
https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/
vi /etc/apt/sources.list
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main #restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates #main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports #main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
更新软件包索引：
apt update
apt upgrade
apt full-upgrade
apt-get update
允许apt通过HTTPS使用仓库：
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
添加阿里云的Docker官方GPG密钥：
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
向sources.list添加Docker仓库地址：
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
再次更新软件包索引：
sudo apt-get update
安装最新版本的Docker CE：
sudo apt-get install docker-ce
配置Docker镜像加速服务：
sudo tee /etc/docker/daemon.json <<EOF
{
	"registry-mirrors": ["https://docker.ricefox.love/"]
}
EOF
重启Docker服务以应用配置：
sudo systemctl daemon-reload
sudo systemctl restart docker



//直接安装

apt install docker.io