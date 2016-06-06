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

First Test output : 
    bash: host: command not found
so 
	yum install bind-utils
and then
	host ec2-52-17-99-190.eu-west-1.compute.amazonaws.com
result
	ec2-52-17-99-190.eu-west-1.compute.amazonaws.com has address 172.31.34.109
Plus 

 


