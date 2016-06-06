1. Check vm.swappiness on all your nodes

    vi /proc/sys/vm/swappiness

Set the value to 1 if necessary

    sudo su
    echo "vm.swappiness = 1" >> /etc/sysctl.conf

Comments: 

-Permission denied on the current user ec2-user

-done on 5 nodes


2. Set noatime on any non-root volumes you have

Nodes are EBS volumes/ no non-root volumes


 


