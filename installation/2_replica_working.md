## MySQL installation - Plan Two Detail ##

Before installing MySQL latest version, check the supported databases with cloudera manager.( MySQL 5.6 is supported) 

Download the MySQL RPM using wget (all nodes)

	sudo install wget -y
	
	wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm 

Adding the rpm to the repository (all nodes)

	yum localinstall mysql-community-release-el7-5.noarch.rpm

Selecting a release version

	yum repolist all | grep mysql

Result

	mysql56-community/x86_64                                    MySQ enabled:    244

Comment:Version 5.6 is enabled by default, no changes needed.

Installing MySQL server (on the egde node - 90 and on the replica 91)
	
	sudo yum install mysql-community-server

Result

	Installed:
	mysql-community-libs.x86_64 0:5.6.31-2.el7
    mysql-community-server.x86_64 0:5.6.31-2.el7

Installing MySQL client (on all nodes)

	sudo yum install mysql

Result

	Installed:
	  mysql-community-client.x86_64 0:5.6.31-2.el7
      mysql-community-libs.x86_64 0:5.6.31-2.el7


Download and Copy(unzip) MySQL JDBC connectors (all nodes)

	wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.39.tar.gz 

	tar -zxvf mysql-connector-java-5.1.39.tar.gz


## Replication ##

Configure MySQL for replication

[http://www.tecmint.com/how-to-setup-mysql-master-slave-replication-in-rhel-centos-fedora/](http://www.tecmint.com/how-to-setup-mysql-master-slave-replication-in-rhel-centos-fedora/)

running *mysql install db* on Master and Replica nodes

	mysql_install_db --user=mysql

Starting mysqld

	service mysqld start


    mysql> show master status;
    +------------------+----------+--------------+------------------+-------------------+
    | File | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
    +------------------+----------+--------------+------------------+-------------------+
    | mysql-bin.000003 | 2221 | cmdb |  |   |
    +------------------+----------+--------------+------------------+-------------------+
    1 row in set (0.00 sec)
    

In the replica node 

	mysql>CHANGE MASTER TO MASTER_HOST='172.31.34.107', MASTER_USER='root', MASTER_PASSWORD='root', MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=2221;





Result for SLAVE STATUS

`mysql> show slave status \g;
+----------------------+---------------+-------------+-------------+---------------+------------------+---------------------+-------------------------+---------------+-----------------------+------------------+-------------------+-----------------+---------------------+--------------------+------------------------+-------------------------+-----------------------------+------------+------------+--------------+---------------------+-----------------+-----------------+----------------+---------------+--------------------+--------------------+--------------------+-----------------+-------------------+----------------+-----------------------+-------------------------------+---------------+---------------+----------------+----------------+-----------------------------+------------------+-------------+----------------------------+-----------+---------------------+-----------------------------------------------------------------------------+--------------------+-------------+-------------------------+--------------------------+----------------+--------------------+--------------------+-------------------+---------------+
| Slave_IO_State       | Master_Host   | Master_User | Master_Port | Connect_Retry | Master_Log_File  | Read_Master_Log_Pos | Relay_Log_File          | Relay_Log_Pos | Relay_Master_Log_File | Slave_IO_Running | Slave_SQL_Running | Replicate_Do_DB | Replicate_Ignore_DB | Replicate_Do_Table | Replicate_Ignore_Table | Replicate_Wild_Do_Table | Replicate_Wild_Ignore_Table | Last_Errno | Last_Error | Skip_Counter | Exec_Master_Log_Pos | Relay_Log_Space | Until_Condition | Until_Log_File | Until_Log_Pos | Master_SSL_Allowed | Master_SSL_CA_File | Master_SSL_CA_Path | Master_SSL_Cert | Master_SSL_Cipher | Master_SSL_Key | Seconds_Behind_Master | Master_SSL_Verify_Server_Cert | Last_IO_Errno | Last_IO_Error | Last_SQL_Errno | Last_SQL_Error | Replicate_Ignore_Server_Ids | Master_Server_Id | Master_UUID | Master_Info_File           | SQL_Delay | SQL_Remaining_Delay | Slave_SQL_Running_State                                                     | Master_Retry_Count | Master_Bind | Last_IO_Error_Timestamp | Last_SQL_Error_Timestamp | Master_SSL_Crl | Master_SSL_Crlpath | Retrieved_Gtid_Set | Executed_Gtid_Set | Auto_Position |
+----------------------+---------------+-------------+-------------+---------------+------------------+---------------------+-------------------------+---------------+-----------------------+------------------+-------------------+-----------------+---------------------+--------------------+------------------------+-------------------------+-----------------------------+------------+------------+--------------+---------------------+-----------------+-----------------+----------------+---------------+--------------------+--------------------+--------------------+-----------------+-------------------+----------------+-----------------------+-------------------------------+---------------+---------------+----------------+----------------+-----------------------------+------------------+-------------+----------------------------+-----------+---------------------+-----------------------------------------------------------------------------+--------------------+-------------+-------------------------+--------------------------+----------------+--------------------+--------------------+-------------------+---------------+
| Connecting to master | 172.31.34.107 | root        |        3306 |            60 | mysql-bin.000003 |                2221 | mysqld-relay-bin.000001 |             4 | mysql-bin.000003      | Connecting       | Yes               |                 |                     |                    |                        |                         |                             |          0 |            |            0 |                2221 |             120 | None            |                |             0 | No                 |                    |                    |                 |                   |                |                  NULL | No                            |             0 |               |              0 |                |                             |                0 |             | /var/lib/mysql/master.info |         0 |                NULL | Slave has read all relay log; waiting for the slave I/O thread to update it |              86400 |             |                         |                          |                |                    |                    |                   |             0 |
+----------------------+---------------+-------------+-------------+---------------+------------------+---------------------+-------------------------+---------------+-----------------------+------------------+-------------------+-----------------+---------------------+--------------------+------------------------+-------------------------+-----------------------------+------------+------------+--------------+---------------------+-----------------+-----------------+----------------+---------------+--------------------+--------------------+--------------------+-----------------+-------------------+----------------+-----------------------+-------------------------------+---------------+---------------+----------------+----------------+-----------------------------+------------------+-------------+----------------------------+-----------+---------------------+-----------------------------------------------------------------------------+--------------------+-------------+-------------------------+--------------------------+----------------+--------------------+--------------------+-------------------+---------------+
1 row in set (0.00 sec)
`
