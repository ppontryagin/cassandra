Run instructions
=============

# .bash_profile:

export GIRAPH_CORE_JAR=/usr/local/giraph/giraph-core/target/giraph-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar
export GIRAPH_EXAMPLES_JAR=/usr/local/giraph/giraph-core/target/giraph-examples-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar
export GORA_CASSANDRA_JAR=/usr/local/giraph/giraph-gora/conf/apache-gora-0.5/gora-tutorial/lib/gora-cassandra-0.5.jar
export CASSANDRA_JAR=/usr/share/dse/cassandra/lib/cassandra-all-2.0.8.39.jar.

export HADOOP_CLASSPATH=$GIRAPH_CORE_JAR:$GIRAPH_EXAMPLES:$GIRAPH_GORA_JAR:$GORA_CASSANDRA_JAR
export JAVA_HOME=/usr

export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:giraph-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar:giraph-examples-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar
export DISPLAY=127.0.0.1:0.0

# Запуск на CFS

- run cmd 

dse hadoop jar giraph-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar org.apache.giraph.GiraphRunner \ 
-Dgiraph.SplitMasterWorker=true -Dgiraph.maxNumberOfSupersteps=5 -Dgiraph.logThreadLayout \
 -Dgiraph.zkList=SRV2-ITSD03:22181,SRV2-ITSD04:22181,SRV2-ITSD05:22181,SRV2-ITSD06:22181,SRV2-ITSD07:22181,SRV2-ITSD08:22181 
 \ -D mapreduce.map.log.level=TRACE  -libjars giraph-examples-1.1.0-SNAPSHOT-for-hadoop-1.2.1-jar-with-dependencies.jar \ 
 org.apache.giraph.examples.SimpleShortestPathsComputation -vip /user/hduser/input/short.txt \ 
 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /user/hduser/output/short.txt -w 3
 
# Запуск на Hive

dse hadoop jar giraph-hive-1.1.0-SNAPSHOT.jar org.apache.giraph.hive.HiveGiraphRunner -computationClass org.apache.giraph.examples.SimpleShortestPathsComputation \ 
-w 5 -vi "org.apache.giraph.hive.input.vertex.examples.HiveIntDoubleDoubleVertex, test1" -hiveconf hive.metastore.uris=thrift://localhost:10000
 
# To del : for git
# To del: check RHEL stand integration