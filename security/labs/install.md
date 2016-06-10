Install kerberos server on CM Server
 	
	yum install krb5-server krb5-libs krb5-auth-dialog

Install kerberos client all nodes 

	yum install krb5-workstation krb5-libs krb5-auth-dialog

For SSO

	yum install krb5-pkinit-openssl

Edit the /etc/krb5.conf and /var/kerberos/krb5kdc/kdc.conf configuration files

	see  files in the lab folder

create a database  that stores keys for the Kerberos realm

	/usr/sbin/kdb5_util create -s

root is the password

Create a linux user: waelbou
	useradd waelbou
	passwd wael
	root123admin

add the first principal for waelbou

	/usr/sbin/kadmin.local -q "addprinc waelbou/admin@HADOOP.COM"
pwd: root