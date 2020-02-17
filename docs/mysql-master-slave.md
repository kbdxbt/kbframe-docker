### mysql主从配置
> 使用前前确保kbframe-docker安装环境成功，并启动了 mysql_master 和 mysql_slave

1.进入mysql_master命令行
- 可通过navicat直接连接mysql_master执行命令行
- 可以通过docker容器进入 docker exec -it mysql_master /bin/bash，执行mysql连接命令进入命令行模式
2.确保开启二进制文件，执行下面命令查看
```
show variables like 'log_%';
```
3.创建slave账号并设置权限：
```
CREATE USER 'slave'@'%' IDENTIFIED BY '123456';
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'slave'@'%';
```
4.记录master的相关信息配置信息，File和Position
```
show master status; 
```
5.进入mysql_slave命令行，替换并执行下面语句
```
change master to 
    master_host='[你的ip]', 
    master_user='slave', 
    master_password='123456', 
    master_port=3307, 
    master_log_file='[mysql-bin日志文件]', 
    master_log_pos=[master position], 
    master_connect_retry=30;
```
6.启动slave
```
start slave;
```
7.查看执行状态，Slave_IO_Running和Slave_SQL_Running均为Yes即表示配置成功
```
show slave status;
```