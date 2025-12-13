---
title: "docker部署gitlab"
tags: docker
---



#### 创建容器
```
docker pull gitlab/gitlab-ce
mkdir /usr/local/share/applications/gitlab

docker run -itd  \
 -p 8980:80 \
 -p 8922:22 \
 -v /usr/local/share/applications/gitlab/etc:/etc/gitlab  \
 -v /usr/local/share/applications/gitlab/log:/var/log/gitlab \
 -v /usr/local/share/applications/gitlab:/var/opt/gitlab \
 --restart always \
 --privileged=true \
 --name gitlab \
 gitlab/gitlab-ce
```
#### 修改配置文件

```
docker exec -it gitlab /bin/bash
vi /etc/gitlab/gitlab.rb

#开头添加以下配置
#gitlab访问地址
external_url 'http://#域名'
#ssh主机地址
gitlab_rails['gitlab_ssh_host'] = '#域名'
#ssh连接端口(外部端口非容器内端口)
gitlab_rails['gitlab_shell_ssh_port'] = 9922
#时区
gitlab_rails['time_zone'] = 'Asia/Shanghai'
#开启备份功能
gitlab_rails['manage_backup_path'] = true
#备份文件的权限
gitlab_rails['backup_archive_permissions'] = 0644
#保存备份 60 天
gitlab_rails['backup_keep_time'] = 5184000

修改ssh端口
vi /etc/ssh/sshd_config
Port 8922

```
#### 添加邮箱(可选)
```
docker exec -it gitlab /bin/bash
vi /etc/gitlab/gitlab.rb

gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = 'smtphz.qiye.163.com'
gitlab_rails['smtp_port'] = 465
gitlab_rails['smtp_user_name'] = '#发信邮箱地址'
gitlab_rails['smtp_password'] = '#邮箱密码'
gitlab_rails['smtp_domain'] = 'smtphz.qiye.163.com'
gitlab_rails['smtp_authentication'] = 'login'
gitlab_rails['smtp_enable_starttls_auto'] = false
gitlab_rails['smtp_tls'] = true
gitlab_rails['smtp_pool'] = '#发信邮箱地址'
gitlab_rails['gitlab_email_enabled'] = true
gitlab_rails['gitlab_email_from'] = '#发信邮箱地址'

#测试邮箱
gitlab-ctl reconfigure
gitlab-rails console
Notify.test_email('#收信邮箱地址', 'GitLab email', 'Hellow world').deliver_now
```

#### 刷新配置
```
# 获取初始密码
cat /etc/gitlab/initial_root_password 
jKWHmRhgmHc44hUAzqXql5+UmrB6xblKZSK2qC9mnLU=

#刷新配置
gitlab-ctl reconfigure
gitlab-ctl restart
exit;
```

#### 客户端设置

```
#生成ssh秘钥复制到gitlab绑定
ssh-keygen
cat ~/.ssh/id_rsa.pub
```



