## �ק�Hostname
- sudo hostname master (�bmaster�W)
- sudo hostname slave1 (�bslave1�W)
- sudo hostname slave2 (�bslave2 �W)
- sudo hostname slave3 (�bslave3 �W)

## �ק� /etc/hosts (sudo vi /etc/hosts)
- �ϥ�ifconfig �ˬd�U�۪�IP
```
192.168.161.133 master
192.168.161.134 slave1
192.168.161.135 slave2
192.168.161.136 slave3
```
### �ק�]�w�� (�b/usr/local/hadoop/etc/hadoop/)
- vi hdfs-site.xml 
```
 <property>
    <name>dfs.replication</name>
    <value>3</value>
  </property>
```
 
- vi core-site.xml
```
 <property>
    <name>fs.defaultFS</name>
    <value>hdfs://master</value>
  </property>
```

## �ƻs�]�w��
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave1:/usr/local/hadoop/etc/hadoop/
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave2:/usr/local/hadoop/etc/hadoop/
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave3:/usr/local/hadoop/etc/hadoop/

- vi slaves
```
slave1
slave2
slave3
```

### �榡��HDFS
- hdfs namenode -format

### �ҥ�HDFS
- start-dfs.sh

## �ק�t�m���G�n�J Master �q���ӭק�]�w >
- regionservers # �]�w regionservers
- backup-masters # �]�w backup master
- hbase-site.xml # �]�w Configure ZooKeeper

### regionservers ( $HBASE_HOME/conf/regionservers )

- master
- slave1
- slave2
- slave3

### backup-masters ( $HBASE_HOME/conf/backup-masters )
- slave1

### hbase-site.xml ( $HBASE_HOME/conf/hbase-site.xml )
```
<configuration>
  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value>
  </property>
  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://master:8020/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.quorum</name>
    <value>master,slave1,slave2,slave3</value>
  </property>
  <property>
    <name>hbase.tmp.dir</name>
    <value>/home/hadoop/hadoop/hbase-tmp</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/hadoop/hadoop/zookeeper</value>
  </property>
</configuration>
```
### �ƻs�t�m��Ҧ�nodes�G
- scp -r $HBASE_HOME/conf hadoop@slave1:/usr/local/hbase/conf
- scp -r $HBASE_HOME/conf hadoop@slave2:/usr/local/hbase/conf
- scp -r $HBASE_HOME/conf hadoop@slave3:/usr/local/hbase/conf


### ���� Hadoop
- stop-dfs.sh 

### ���� Hadoop 
- start-dfs.sh

### ���� HBase
- stop_hbase.sh 

### ���� HBase 
- start_hbase.sh
