# docker-mysql-master-slave  
docker-mysql-master-slave  

首先，连接 master ，查找 binlog 文件名称和 pos  
master command  
show binary logs;  
show master status;  

第二步，连接 slave ，设置要连接的 master 参数  
slave command  
CHANGE MASTER TO MASTER_HOST='10.0.75.1',  
MASTER_LOG_FILE='mysql-bin.000003',  
MASTER_USER='root',  
MASTER_PASSWORD='a.123456',  
MASTER_LOG_POS=154;  

第三步，启动 slave，查看 slave 状态  
start slave;  
show slave status;  

调试命令  
debug command  
slave command; 
stop slave;  
reset slave;  

note:  
连接命令只有第一次启动需要输入  
mysql 5.7 版本 8.0版本都可用  
relay_log 有文章说需要这个参数我就加上了
mysql-origin 作为多级别主从，log_slave_updates=1 配置已经加上
数据流向 origin -> master -> slave,  master->slave  

log:  
master 关闭重启后，slave 连接一直等待中，4次自动连接后，再次连接上 master  
