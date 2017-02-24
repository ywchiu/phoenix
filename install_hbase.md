
### 安裝 HBase 環境

- wget http://apache.stu.edu.tw/hbase/1.2.4/hbase-1.2.4-src.tar.gz
- tar -zxvf hbase-1.2.4-bin.tar.gz
- sudo mv hbase-1.2.4 /usr/local/hbase
- sudo chown -R hadoop:hadoop /usr/local/hbase
- sudo chmod +x -R /usr/local/hbase

### 修改環境變數 (vi ~/.bashrc)
- export HBASE_HOME=/usr/local/hbase
- export PATH=$PATH:$HBASE_HOME/bin

### 修改hbase-env.sh
- vim $HBASE_HOME/conf/hbase-env.sh  # 修改 JAVA_HOME 路徑

```
/usr/java/jdk1.8.0_102/
```

### 修改設定檔
- vi /usr/local/hbase/conf/hbase-site.xml

```
<configuration>
  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value>
  </property>
  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://localhost:8020/hbase</value>
  </property>
</configuration>
```

## 啟用HBase
- start-hbase.sh
