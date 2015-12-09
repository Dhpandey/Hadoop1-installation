# Hadoop1-installation(Single node setup)

Note : Applied only for Hadoop1 . 
Hadoop2 needs different setting and configuration  

Installation steps with demo for hadoop 1.2.1

#Prerequisites
  Os: Linux
  
 jdk 1.6 and above

Download hadoop-1.2.1.jar

  Source: https://archive.apache.org/dist/hadoop/core/hadoop-1.2.1/

#SINGLE-NODE INSTALLATION

Step 1 :Install jdk 1.6 or above and
confirm 

     $java -version

Step 2: Adding a dedicated Hadoop system user(optional)

    $ sudo addgroup hadoop_group

    $ sudo adduser --ingroup hadoop_group hadoopuser1

Step 3 :Add hadoopuser1 to hadoop_group (optional)

     $sudo adduser hduser1 sudo


Step 4 : Configuring SSH

 step 4.1 : Generate SSH key for hadoopuser1

   switch to hadoopuser1 : $su – hadoopuser1 (optional)

Generate ssh key

     $ssh-keygen -t rsa -P ""   press Enter

This creates  an RSA key pair with an empty password. (-p “ ”)

 Step 4.2 : Enable SSH access to local machine with this newly created key

     $cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys

Test:

    $ssh localhost

shows some log for successful connection

#Main Installation

(confirm you are in same user )

Step 5 : Add following to .bashrc

     export HADOOP_HOME=/opt/hadoop (location of hadoop)

     export PATH=$PATH:$HADOOP_HOME/bin

Step 6: Now we create the directory and set the required ownerships and permissions

     $sudo mkdir -p /app/hadoop/tmp

     $sudo chown hadoopuse1r:hadoop_group /app/hadoop/tmp (optional if you create user and group)

     $sudo chmod 750 /app/hadoop/tmp

#Configuration
Step 7 : Changes in following files inside hadoop/conf 
(copy from above configuration or download from https://github.com/Dhpandey/Hadoop1-installation.git)

     hadoop-env.sh

     core-site.xml

     mapred-site.xml

     hdf-site.xml

Step 8:

Format Namenode(dont do several times)

     $hadoop namenode -format

Check log carefully , you must see successfully formated in the log

 
 Ready  now
 
#RUN:
Step 8 :

Start all the services:

       start-all.sh

stop all the services:

       stop-all.sh

#Test 
Namenode:

      localhost:50070

JobTracker:

      localhost:50030
      
      
    

 ##########################################################################
  
#Steps to run first program using hadoop

Running MapReduce job

Step 1:
      $mkdir javafolder
            
//to store compiled java classes

Step 2:
      Download hadoop-core-version.jar

Step 3: 
      Ceate jar file:

      $javac -classpath hadoop-core-version.jar -d javafolder test.java
      $jar -cvf  test.jar -C javafolder/ .

Step 4:
  create  input directory in hdfs:

      $hadoop fs -mkdir inputfolder

Step5 :
  Copy input data from local to hdfs direcrtory:

      $hadoop fs -put  inputdata.txt inputdata.txt inputfolder

Step 6:
  RUN  command
    $hadoop jar test.jar package.className inputfolder outputfolder

Track the process in jobtracker :localhost:50030
and check the output in ouputfolder if all completed


