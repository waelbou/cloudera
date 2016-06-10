install rpm
	rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el6-8.noarch.rpm

specify mysql version

	vi  /etc/yum.repos.d/mysql-community.repo


install mysql server

	yum install mysql-community-server

Command
	yum repolist enabled
Content

Loaded plugins: fastestmirror, presto
Loading mirror speeds from cached hostfile
 * base: ftp.heanet.ie
 * extras: ftp.heanet.ie
 * updates: ftp.heanet.ie
repo id                                                         repo name                                                        status
base                                                            CentOS-6 - Base                                                  6696
extras                                                          CentOS-6 - Extras                                                  60
mysql-connectors-community                                      MySQL Connectors Community                                         21
mysql-tools-community                                           MySQL Tools Community                                              35
mysql-tools-preview                                             MySQL Tools Preview                                                 3
mysql55-community                                               MySQL 5.5 Community Server                                        265
mysql57-community                                               MySQL 5.7 Community Server                                         98
updates                                                         CentOS-6 - Updates                                                115

Password mysql 

	%E:rN:f#H2u7