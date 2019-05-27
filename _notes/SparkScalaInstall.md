My Spark Environment
http://192.168.0.32:4040/jobs/

My Ubuntu Spark/Scala Setup
--------------------------
My notes on how to set up Spark/Scala environment. This uses dotty scala 3.0 which has not been released yet.

Spark:  spark-2.4.3
Java:   openjdk-8-jdk
        Later versions could be issue for cansandra
Scala:  dotty-0.14.0-RC1
        Must be > 0.13.0-RC1 (1st 3.0 version to support spark)
SBT:    sbt-1.2.8
Cassandra: 
VSCode: 

**Spark Installation**
Step 1: Download Spark
----------------------
wget http://apache.claz.org/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz

Step 2: Place uncompressed Spark  
-------------------------------
tar -xzf spark-2.4.3-bin-hadoop1.tgz
sudo mkdir /home/hadoop
sudo mkdir /home/hadoop/work
mv spark-2.4.3.tgz /home/hadoop/work/spark-2.4.3-bin-hadoop2.7

Step 3: Modify your .bashrc to include path to include Spark
----------------------------------------------------------
vi ~/.bashrc
export SPARK_HOME=/home/hadoop/work/spark-2.4.3-bin-hadoop2.7
export PATH=$PATH:$SPARK_HOME/bin

Step 4: Configure /conf/spark-env.sh
-----------------------------------
cd conf
cp spark.env.sh.template spark-env.sh

/conf/spar-env.sh
export SPARK_MASTER_IP=<ip here>
export SPARK_WORKER_CORES=1
export SPARK_MEMORY=1g
export SPARK_WORKER_INSTANCES=2
export SPARK_WORKER_DIR=/home/home/spark_work_Dir

**Java Installation**

Step 1: Default open jdk 8
--------------------------
sudo apt install openjdk-8-jdk
 
**Scala Installation**

Step 1: Download Scala
---------------------
wget https://github.com/lampepfl/dotty/releases/download/0.14.0-RC1/dotty-0.14.0-RC1.tar.gz
 

Step 2: Place uncompressed Scala into /home/hadoop
-------------------------------------------
tar -xvf dotty-0.14.0-RC1.tar.gz
sudo mv dotty-0.14.0-RC1 /home/hadoop/work/dotty-0.14.0-RC1

Step 3: Install for other tooling
--------------------------------
sudo apt-get install scala

Step 4: Install SBT
-------------------
https://piccolo.link/sbt-1.2.8.tgz

Step 5: Modify .bashrc to include path to include Scala
------------------------------------------------------
vi ~/.bashrc
export SCALA_HOME=/home/hadoop/work/dotty-0.14.0-RC1
export PATH=$PATH:$SCALA_HOME/bin

**Casandra**
Step 1: Update PPA
echo "deb http://www.apache.org/dist/cassandra/debian 311x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list 

curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add - 

Step 2: Manually add key and update
sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA
sudo apt-get update 

Step 3: Install
sudo apt-get install cassandra  

**Spark Cansandra Connector**
Step 1: Install via spark-shell
$SPARK_HOME/bin/spark-shell --packages datastax:spark-cassandra-connector:2.4.0-s_2.11

More Info::
https://github.com/datastax/spark-cassandra-connector/

**Test Launch**
Step 1: Launch spark-shell
-------------------------
spark-shell

Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.4.3
      /_/

Using Scala version 2.11.12 (OpenJDK 64-Bit Server VM, Java 11.0.3)
Type in expressions to have them evaluated.
Type :help for more information.

scala> 

Step 2: Launch scala
--------------------
scala

Welcome to Scala 2.11.12 (OpenJDK 64-Bit Server VM, Java 11.0.3).
Type in expressions for evaluation. Or try :help.

scala>  

Step 3: Launch dotc
-------------------
dotc -version

Dotty compiler version 0.14.0-RC1 -- Copyright 2002-2019, LAMP/EPFL

Step 4: Launch SBT
------------------
sbt

References
----------
http://www.codebind.com/linux-tutorials/install-scala-sbt-java-ubuntu-16-04/
https://www.youtube.com/watch?v=BozSL9ygUto

https://spark.apache.org/downloads.html
