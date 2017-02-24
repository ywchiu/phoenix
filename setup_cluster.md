## 修改 /etc/hosts

## 修改Hostname
- hostname master (在master上)
- hostname slave1 (在slave1上)
- hostname slave2 (在slave2 上)
- hostname slave3 (在slave3 上)

## 修改配置文件：登入 Master 電腦來修改設定 >
- regionservers # 設定 regionservers
- backup-masters # 設定 backup master
- hbase-site.xml # 設定 Configure ZooKeeper

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
### 複製配置到所有nodes：
- scp -r $HBASE_HOME/conf hadoop@slave1:/usr/local/hbase/conf
- scp -r $HBASE_HOME/conf hadoop@slave2:/usr/local/hbase/conf
- scp -r $HBASE_HOME/conf hadoop@slave3:/usr/local/hbase/conf


### 關閉 Hadoop
- stop-dfs.sh 

### 執行 Hadoop 
- start-dfs.sh

### 關閉 HBase
- stop_hbase.sh 

### 執行 HBase 
- start_hbase.sh
