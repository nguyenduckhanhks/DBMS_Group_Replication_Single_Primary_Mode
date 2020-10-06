# DBMS_Group_Replication_Single_Primary_Mode
# Config trên terminal:
# Config chung:

$ mysql -u root
mysql> SET SQL_LOG_BIN=0;
mysql> CREATE USER 'repl'@'%' IDENTIFIED BY 'password' REQUIRE SSL;
mysql> GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%'; 
mysql> FLUSH PRIVILEGES;
mysql> SET SQL_LOG_BIN=1;

mysql> CHANGE MASTER TO MASTER_USER='repl', MASTER_PASSWORD='password' FOR CHANNEL 'group_replication_recovery';

mysql> INSTALL PLUGIN group_replication SONAME 'group_replication.so';
mysql> SHOW PLUGINS;

# Config primary server:
mysql> SET GLOBAL group_replication_bootstrap_group=ON;
mysql> START GROUP_REPLICATION;
mysql> SET GLOBAL group_replication_bootstrap_group=OFF;

# Config secondary server 

mysql> START GROUP_REPLICATION;
