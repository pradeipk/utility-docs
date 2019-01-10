# Tools and commands





### Table of Contents
1. [HBase](#HBase)
2. [Hadoop](#Hadoop)
3. [Flink](#Flink)
4. [Couchbase](#Couchbase)








## HBase

``Overview``

1. HBase is a distributed column-oriented database built on top of the Hadoop file system. It is an open-source project and is horizontally scalable.
2. It is a part of the Hadoop ecosystem that provides random real-time read/write access to data in the Hadoop File System.
3. Hadoop can perform only batch processing, and data will be accessed only in a sequential manner. That means one has to search  the entire dataset even for the simplest of jobs. A huge dataset when processed results in another huge data set, which should also be processed sequentially. At this point, a new solution is needed to access any point of data in a single unit of time (random access) and HBase is the solution.

``Installation``

> https://www.tutorialspoint.com/hbase/hbase_installation.htm

> https://www.guru99.com/hbase-installation-guide.html

1. download
2. unzip
3. run D:\hbase-1.2.9\bin> start-hbase.sh or start-hbase.cmd
4. ./bin/stop-hbase.sh
    exit
Three Mode Of installation:

1. Standalone mode installation (No dependency on Hadoop system)
    - This is default mode of HBase
    - It runs against local file system
    - It doesn't use Hadoop HDFS
    - Only HMaster daemon can run
    - Not recommended for production environment
    - Runs in single JVM

2. Pseudo-Distributed mode installation ( Single node Hadoop system + HBase installation)
    - It runs on Hadoop HDFS
    - All Daemons run in single node
    - Recommend for production environment
    
3. Fully Distributed mode installation ( MultinodeHadoop environment + HBase installation)
    - It runs on Hadoop HDFS
    - All daemons going to run across all nodes present in the cluster
    - Highly recommended for production environment


``Working With Hbase``

- Start HBase Shell 
  You can start HBase shell using the following command.

  command from dir bin> hbase shell
  
  hbase(main):003:0>

  $cd bin
  $./hbase shell
  This will give you the HBase Shell Prompt as shown below.


``Pre-requsite``






``Shell Commands``


1. a.drop_all ‘t.*’ 
   b.disable_all 'raj.* 
2. disable 'emp'
3. drop 'emp'
4. Create		This command creates a table.
5. List			It lists all the tables in HBase.
6. Disable		This command disables a table.
7. Is_disabled	Whereas, it verifies whether a table is disabled.
8. enable		This command enables a table.
9. Is_enabled	However, it verifies whether a table is enabled or not.

Let’s discuss Books for HBase

10. Describe	It shows the description of a table. ---> describe 'table_name'
11. Alter		This command alters a table.
12. Exists		This one verifies whether a table exists or not.
13. Drop			This command drops a table from HBase.
14. Drop_all	Whereas,  this command drops the tables matching the ‘regex’ given in the command.
15. get 'pradeip','r',{COLUMN => 'name'}
16. scan 'pradeip', {COLUMN => 'name:first'}
 
 

``References``

1. https://www.tutorialspoint.com/hbase




## Flink

https://flink.apache.org/

1. root@pradeip3785:~/flink-1.6.3# bin/start-cluster.sh
2. run a jar: root@pradeip3785:~/flink# bin/flink run examples/batch/WordCount.jar -input /home/dataflair/input.txt -output /home/dataflair/output.txt

To stop Flink when you’re done type:

$ ./bin/stop-cluster.sh

https://dzone.com/articles/apache-flink-basic-transformation-example





