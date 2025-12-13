---
title: "ubuntu安装java多版本灵活切换"
tags: ubuntu
---



安装多版本

```
sudo apt install openjdk-8-jdk
sudo apt install openjdk-11-jdk
sudo apt install openjdk-17-jdk
java -version
```
找到安装路径
```
cd /
find / -name java
/usr/lib/jvm/java-8-openjdk-amd64/bin/java
/usr/lib/jvm/java-11-openjdk-amd64/bin/java
/usr/lib/jvm/java-17-openjdk-amd64/bin/java

```
添加安装路径

```
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-8-openjdk-amd64/bin/java 100
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-11-openjdk-amd64/bin/java 100
```

选择JDK版本
```
sudo update-alternatives --config java
```
~~添加环境变量~~


```
sudo vim /etc/environment
在最后一行，添加确定版本的JAVA_HOME

#这一行是文件原本就有的
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/

立即生效，并查看结果
source /etc/environment
echo $JAVA_HOME
```