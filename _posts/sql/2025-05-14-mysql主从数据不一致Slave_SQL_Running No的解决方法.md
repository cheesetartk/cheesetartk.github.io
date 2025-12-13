---
title: "mysql主从数据不一致Slave_SQL_Running No的解决方法"
tags: sql
---



在slave服务器上通过如下命令

```
mysql> show slave status\G;
```

显示如下情况：

> Slave_IO_Running: Yes
> Slave_SQL_Running: No

表示slave不同步

**解决方法一(忽略错误，继续同步)：**

1、先停掉slave

```
mysql> stop slave;
```

2、跳过错误步数，后面步数可变

```
mysql> set global sql_slave_skip_counter=1;
```

3、再启动slave

```
mysql> start slave;
```

4、查看同步状态

```
mysql> show slave status\G;
```

**解决方法二(重新做主从，完全同步)：**

1、先进入主库进行锁表，注意窗口不要关闭

```
mysql> flush table with read lock;
```

2、把数据进行备份

```
> mysqldump -uroot -p --opt -R 数据库 > /data/bak.sql
```

3、再新开个窗口，查看主数据库信息

```
mysql> show master status;` `+``------------------+----------+--------------+------------------+-------------------+``| File    | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |``+``------------------+----------+--------------+------------------+-------------------+``| mysql-bin.000005 |  1158 |    |     |     |``+``------------------+----------+--------------+------------------+-------------------+
```

4、在从库上停止slave

```
mysql> stop slave;
```

5、导入备份的数据文件

```
mysql> source /data/bak.sql
```

6、重置同步

```
mysql> reset slave;
```

7、重新设置同步节点

```
mysql> CHANGE MASTER TO
MASTER_HOST='192.168.137.233',
MASTER_PORT=3306,
MASTER_USER='sync',
MASTER_PASSWORD='123456',
MASTER_LOG_FILE='mysql-bin.000005',
MASTER_LOG_POS=1158;
```

host，port，user，password请根据你的主库设置相应修改，log_file和log_pos根据主库中master status相应修改。

8、开启slave

```
mysql> start slave;
```

9、查看slave状态

```
mysql> show slave status\G;
```

显示如下信息则表示正常

> Slave_IO_Running: Yes
> Slave_SQL_Running: Yes

10、对主数据库解锁

```
mysql> unlock tables;
```

11、再次在主库中添加或修改数据，看从库数据是否同步。