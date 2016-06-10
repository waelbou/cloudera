OS Info

	vi /etc/centos-release

Content

	CentOS release 6.8 (Final)

FQDN for the MySQL Server

	ec2-52-19-152-64.eu-west-1.compute.amazonaws.com


yum

	yum repolist enabled

Output

Loaded plugins: fastestmirror, presto
Loading mirror speeds from cached hostfile
 * base: centos.serverspace.co.uk
 * extras: centos.serverspace.co.uk
 * updates: centos.hyve.com
repo id                                                    repo name                                                             status
base                                                       CentOS-6 - Base                                                       6696
extras                                                     CentOS-6 - Extras                                                       60
updates                                                    CentOS-6 - Updates                                                     115


Accounts

	useradd cameron -u 2500
	useradd johnson -u 2501

	groupadd leave
	groupadd remain

	usermod -a -G leave johnson
	usermod -a -G remain johnson

/etc/passwd
	cameron:x:2500:2500::/home/cameron:/bin/bash
	johnson:x:2501:2501::/home/johnson:/bin/bash

/etc/group

	leave:x:2502:johnson
	remain:x:2503:cameron





