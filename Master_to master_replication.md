# Installing 1_master_mysql and 2_master_mysql on EC2 instances
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234180629-f38e8518-63dd-4eb3-9edb-d29203c80b05.png">

###
# On Master Server 1
###

### Unique ID of the MySQL server. 
### This ID can not be re-used in any nodes in the cluster.
	server-id = 101

<img width="779" alt="image" src="https://user-images.githubusercontent.com/52627259/234180950-28c4f5f9-1281-4bca-8676-2231b4595726.png">

###
### This is the file in which all the replication information is stored.
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
	
### Cheking status 1_master_mysql database
<img width="522" alt="image" src="https://user-images.githubusercontent.com/52627259/234183680-302a76f3-ed60-42b2-b000-1713f751fd84.png">

### Restart mysql-master database
<img width="743" alt="image" src="https://user-images.githubusercontent.com/52627259/234184203-26f817c5-8ed2-461a-8d2f-9a73d60fb0c5.png">

###
# On Master Server 2
###

### Unique ID of the MySQL server. 
### This ID can not be re-used in any nodes in the cluster.
	server-id = 102

<img width="733" alt="image" src="https://user-images.githubusercontent.com/52627259/234182662-26220cd5-84a9-4870-9ab7-a975568dfa9c.png">

###
### This is the file in which all the replication information is stored.
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

### Cheking status 2_master_mysql database
<img width="551" alt="image" src="https://user-images.githubusercontent.com/52627259/234183789-721a413b-8b3a-449f-84e7-ab6b2602d982.png">

### Restart mysql-master database
<img width="740" alt="image" src="https://user-images.githubusercontent.com/52627259/234184447-2ef90d23-54df-45fe-9ed1-10f902b0bed6.png">

### Creating database 'test001' in 1_master_mysql database
<img width="483" alt="image" src="https://user-images.githubusercontent.com/52627259/234185540-7e794fa9-30f3-49d4-a64b-3483dca1f43a.png">

### Cheking database 'test001' in 2_master_mysql database
<img width="557" alt="image" src="https://user-images.githubusercontent.com/52627259/234185623-4c366fad-ebb0-40e6-84ef-3878a45b0776.png">

