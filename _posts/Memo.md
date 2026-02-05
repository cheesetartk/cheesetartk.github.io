---
title: "Memo"
tags: z-other
---

## linux

uname -r 查看内核版本

结果保存到指定的文件
ls > /home/myml.lst 

写入已有文件，追加功能
ls >> /home/myml.lst 

添加more可以翻页
cat /etc/log/messages | more 

添加less可以翻页

less /etc/log/messages 

命令替换  格式为  命令1 '命令2'  其中命令2的输出作为命令1的参数，



添加一个普通用户 （非管理员）的语法格式为  adduser [--home 用户主文件夹] [--shell SHELL] [--no-create-home（无主文件夹）] [--uid  用户ID] [--firstuid ID] [--lastuid ID] [--gecos GECOS] [--ingroup 用户组 | --gid 组ID]  [--disabled-password（禁用密码）] [--disabled-login（禁止登录）] [--encrypt-home] 用户名 



添加一个管理员的语法格式为   adduser --system [--home 用户主文件夹] [--shell SHELL] [--no-create-home （无主文件夹）]  [--uid 用户ID] [--gecos GECOS] [--group | --ingroup 用户组 | --gid 组ID]  [--disabled-password（禁用密码）] [--disabled-login （禁止登录）] 用户名 



用户删除命令deluser在Ubuntu中使用较多。其中，选项--remove-home表示同时删除 用户的主目录和邮箱；--remove-all-files 表示删除用户拥有的所有文件；--backup 表示删除前将文 件备份，--backup-to 指定备份的目标目录（默认是当前目录）；--system表示只有当该用户 是系统用户时才删除。



  /bin：存放用于系统管理维护的常用实用命令文件。    /boot：存放用于系统启动的内核文件和引导装载程序文件。    /dev：存放设备文件。    /etc：存放系统配置文件，如网络配置、设备配置、X Window系统配置等。    /home：各个用户的主目录，其中的子目录名称即为各用户名。    /lib：存放动态链接共享库（其作用类似于Windows里的.dll文件）。    /media：为光盘、软盘等设备提供的默认挂载点。    /mnt：为某些设备提供的默认挂载点。    /root：root 用户主目录。不要将其与根目录混淆。    /proc：系统自动产生的映射。查看该目录中的文件可获取有关系统硬件运行的信息。    /sbin：存放系统管理员或者root用户使用的命令文件。    /usr：存放应用程序和文件。    /var：保存经常变化的内容，如系统日志、打印。 



链接文件有两种类型，分别是符号链接（Symbolic Link）和硬链接（Hard Link）。  符号链接文件类似于 Windows 系统中的快捷方式，其内容是指向原文件的路径。原文件删除后， 符号链接就失效了；删除符号链接文件并不影响原文件。  硬链接是对原文件建立的别名。建立硬链接文件后，即使删除原文件，硬链接也会保留原文件的所 有信息。因为实质上原文件和硬链接是同一个文件，二者使用同一个索引节点，无法区分原文件和硬链 接。与符号链接不同，硬链接和原文件必须在同一个文件系统上，而且不允许链接至目录。

于文本窗口界面的分区工具cfdisk

fdisk -1可列出系统所连接的所有磁盘的基本信息，







