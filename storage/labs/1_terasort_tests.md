## lab   

Creating folders

	[ec2-user@ip-172-31-34-107 ~]$ sudo -u hdfs hadoop fs -mkdir -p /tmp
	[ec2-user@ip-172-31-34-107 ~]$ sudo -u hdfs hadoop fs -mkdir -p /tmp/waelbou
	[ec2-user@ip-172-31-34-107 ~]$ sudo -u hdfs hadoop fs -mkdir -p /tmp/dlxandrzaha
	[ec2-user@ip-172-31-34-107 ~]$ sudo -u hdfs hadoop fs -chmod -R 1777 /tmp

running teragen 

	hadoop jar /opt/cloudera/parcels/CDH-5.7.1-1.cdh5.7.1.p0.11/lib/hue/apps/oozie/examples/lib/hadoop-examples.jar teragen 5000000 /tmp/waelbou/

removing the output directory

	hadoop fs -rm -r -f -skipTrash /tmp/waelbou

Testing sending data to another cluster

	time hadoop distcp hftp://ec2-52-208-1-52.eu-west-1.compute.amazonaws.com:50070/tmp/dlxandrzaha/teragen/part-m-00000 hdfs://ip-172-31-34-107.eu-west-1.compute.internal/tmp/dlxandrzaha/

## Test HDFS performance

creating a 5 gb file with 32mb block size

	time hadoop jar /opt/cloudera/parcels/CDH-5.7.1-1.cdh5.7.1.p0.11/lib/hue/apps/oozie/examples/lib/hadoop-examples.jar teragen -Ddfs.blocksize=32M  50000000 /tmp/performance/


Result

real    1m49.353s
user    0m6.326s
sys     0m0.303s


add a Cache pool

	hdfs cacheadmin -addPool performancepool

add a directive 

	hdfs cacheadmin -addDirective -path /tmp/performance -pool performancepool


run terasort first time 

	time hadoop jar /opt/cloudera/parcels/CDH-5.7.1-1.cdh5.7.1.p0.11/lib/hue/apps/oozie/examples/lib/hadoop-examples.jar terasort /tmp/performance /tmp/terasort-output