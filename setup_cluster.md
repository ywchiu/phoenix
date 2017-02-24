## 修改Hostname
- sudo hostname master (在master上)
- sudo hostname slave1 (在slave1上)
- sudo hostname slave2 (在slave2 上)
- sudo hostname slave3 (在slave3 上)

## 修改 /etc/hosts (sudo vi /etc/hosts)
- 使用ifconfig 檢查各自的IP
```
192.168.161.133 master
192.168.161.134 slave1
192.168.161.135 slave2
192.168.161.136 slave3
```
### 修改設定檔 (在/usr/local/hadoop/etc/hadoop/)
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

## 複製設定檔
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave1:/usr/local/hadoop/etc/hadoop/
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave2:/usr/local/hadoop/etc/hadoop/
- scp /usr/local/hadoop/etc/hadoop/* hadoop@slave3:/usr/local/hadoop/etc/hadoop/

- vi slaves
```
slave1
slave2
slave3
```

### 格式化HDFS
- hdfs namenode -format

### 啟用HDFS
- start-dfs.sh

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
