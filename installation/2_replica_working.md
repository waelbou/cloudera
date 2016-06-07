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


## Replica ##



	
