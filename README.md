# mysql_replication

###
##### On Master Server 1
###

# Unique ID of the MySQL server. 
# This ID can not be re-used in any nodes in the cluster.
server-id = 101
###
# This is the file in which all the replication information is stored.
log-bin = /var/log/mysql/mysql-bin.log

	create user 'rep_user'@'%' identified by 'rep_user_PWD';

	alter user 'rep_user'@'%' identified with mysql_native_password by 'rep_user_PWD';
	
	grant replication slave on *.* to 'rep_user'@'%';
  
  flush privileges;
	
CHANGE MASTER TO MASTER_HOST='IP_of_Master_Server_2',
MASTER_USER='MySQL_user_of_the_Master_Server',
MASTER_PASSWORD='Replication_user_password',
MASTER_LOG_FILE='Log_on_Master_Server_2',
MASTER_LOG_POS=Position_of_log_file_on_Master_Server_2;


###
##### On Master Server 2
###

# Unique ID of the MySQL server. 
# This ID can not be re-used in any nodes in the cluster.
server-id = 102
###
# This is the file in which all the replication information is stored.
log-bin = /var/log/mysql/mysql-bin.log

	create user 'rep_user'@'%' identified by 'rep_user_PWD';

	alter user 'rep_user'@'%' identified with mysql_native_password by 'rep_user_PWD';
	
	grant replication slave on *.* to 'rep_user'@'%';
  
  flush privileges;
	
CHANGE MASTER TO MASTER_HOST='IP_of_Master_Server_1',
MASTER_USER='MySQL_user_of_the_Master_Server',
MASTER_PASSWORD='Replication_user_password',
MASTER_LOG_FILE='Log_on_Master_Server_1',
MASTER_LOG_POS=Position_of_log_file_on_Master_Server_1;
