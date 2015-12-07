# Hadoop1-installation
Note : Hadoop2 needs different setting and configuration  
Installation steps with demo for hadoop 1.2.1

Download 1.2.1
Source: https://archive.apache.org/dist/hadoop/core/hadoop-1.2.1/

#SINGLE-NODE INSTALLATION

Step 1 :Install jdk 1.6 or above and
confirm 

$java -version

Step 2: Adding a dedicated Hadoop system user

$ sudo addgroup hadoop_group

$ sudo adduser --ingroup hadoop_group hadoopuser1

Step 3 :Add hadoopuser1 to hadoop_group 

$sudo adduser hduser1 sudo

Step 4 : Configuring SSH

step 4.1 : Generate SSH key for hadoopuser1

$su – hadoopuser1

$ssh-keygen -t rsa -P ""

This creates  an RSA key pair with an empty password. (-p “ ”)

Step 4.2 : Enable SSH access to local machine with this newly created key

$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys

Test:
$ssh localhost
shows some log of successful connection

Step 5 : #Main Installation
$su - hadoopuser1

Step 6 : Add following to .bashrc

export HADOOP_HOME=/opt/hadoop

export PATH= $PATH:$HADOOP_HOME/bin

Step 6: Now we create the directory and set the required ownerships and permissions

$sudo mkdir -p /app/hadoop/tmp

$sudo chown hduser:hadoop /app/hadoop/tmp

$sudo chmod 750 /app/hadoop/tmp

#Configuration
Step 7 : Changes in following files inside hadoop/conf 
(copy from above configuration)

hadoop-env.sh

core-site.xml

mapred-site.xml

hdf-site.xml

#RUN:
Step 8 :
start:
start-all.sh

stop
stop-all.sh

#Test 
Namenode:

  localhost:50070

JobTracker:

  localhost:50030
