# Check vm.swappiness on all your nodes #

    vi /proc/sys/vm/swappiness

# Set the value to 1 if necessary #

    sudo su
    echo "vm.swappiness = 1" >> /etc/sysctl.conf

Comments: 

-Permission denied on the current user ec2-user

-done on 5 nodes


# Set noatime on any non-root volumes you have #

Nodes are EBS volumes/ no non-root volumes

# Set the reserve space on any non-root volumes to `0` #

Nodes are EBS volumes/ no non-root volumes

# Set the user limits to maximum file descriptors and processes #
descriptors

    echo hdfs - nofile 32768 >> /etc/security/limits.conf
	echo mapred - nofile 32768 >> /etc/security/limits.conf
	echo hbase - nofile 32768 >> /etc/security/limits.conf

processes

	echo hdfs - nproc 32768 >> /etc/security/limits.conf
	echo mapred - nproc 32768 >> /etc/security/limits.conf
	echo hbase - nproc 32768 >> /etc/security/limits.conf

# Test forward and reverse host lookups for correct resolution #

First Test failed : 
    bash: host: command not found
Need to install bind-utils package on all nodes as su
	yum install bind-utils

Testing forward host lookup for all nodes with the public DNS
	
	host ec2-52-51-219-5.eu-west-1.compute.amazonaws.com
	
	host ec2-52-19-168-138.eu-west-1.compute.amazonaws.com

	host ec2-52-50-10-27.eu-west-1.compute.amazonaws.com

	host ec2-52-208-37-55.eu-west-1.compute.amazonaws.com

	host ec2-52-17-99-190.eu-west-1.compute.amazonaws.com

Results for forward host lookup for all nodes with public DNS

	ec2-52-51-219-5.eu-west-1.compute.amazonaws.com has address 172.31.34.107

	ec2-52-19-168-138.eu-west-1.compute.amazonaws.com has address 172.31.34.106

	ec2-52-50-10-27.eu-west-1.compute.amazonaws.com has address 172.31.34.105

	ec2-52-208-37-55.eu-west-1.compute.amazonaws.com has address 172.31.34.104

	ec2-52-17-99-190.eu-west-1.compute.amazonaws.com has address 172.31.34.109

Comment: return only private IPs

Testing forward host lookup for 02 nodes with the private DNS

	host ip-172-31-34-107.eu-west-1.compute.internal
	host ip-172-31-34-106.eu-west-1.compute.internal


Results for forward host lookup for 02 nodes with private DNS

	ip-172-31-34-107.eu-west-1.compute.internal has address 172.31.34.107 
	ip-172-31-34-106.eu-west-1.compute.internal has address 172.31.34.106

Testing reverse host lookup for 02 nodes with public IPs

	host 52.51.219.5
	host 52.19.168.138

Results for reverse host lookup for 02 nodes with public IPs

	5.219.51.52.in-addr.arpa domain name pointer ec2-52-51-219-5.eu-west-1.compute.amazonaws.com.
	138.168.19.52.in-addr.arpa domain name pointer ec2-52-19-168-138.eu-west-1.compute.amazonaws.com.


Testing reverse host lookup for 02 nodes with private IPs

	host 172.31.34.107
	host 172.31.34.106

Results for reverse host lookup for 02 nodes with private IPs

	107.34.31.172.in-addr.arpa domain name pointer ip-172-31-34-107.eu-west-1.compute.internal.
	106.34.31.172.in-addr.arpa domain name pointer ip-172-31-34-106.eu-west-1.compute.internal.

## Verify/enable the nscd service ##

install nscd in all nodes

	sudo yum install nscd

As using RedHat OS we need to disable caching for those services:

passwd, group and netgroup.

	vi /etc/nscd.conf

## Verify/enable the ntpd service ##
install ntpd in all nodes

	sudo yum install ntp
need to restart the node to start the service