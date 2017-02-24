### 修改配置文件：登入 Master 電腦來修改設定 >

regionservers # 設定 regionservers
backup-masters # 設定 backup master
hbase-site.xml # 設定 Configure ZooKeeper
1. regionservers ( $HBASE_HOME/conf/regionservers )

Master
Slave1
Slave2
Slave3
2. backup-masters ( $HBASE_HOME/conf/backup-masters )

Slave1
3. hbase-site.xml ( $HBASE_HOME/conf/hbase-site.xml )

<configuration>
  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value>
  </property>
  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://Master:9000/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.quorum</name>
    <value>Master,Slave1,Slave2,Slave3</value>
  </property>
  <property>
    <name>hbase.tmp.dir</name>
    <value>/home/hduser/hadoop/hbase-tmp</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/hduser/hadoop/zookeeper</value>
  </property>
</configuration>
接下來，將此新的配置，複製到所有nodes：
> $ scp -r $HBASE_HOME hduser@Slave1:~
> $ scp -r $HBASE_HOME hduser@Slave2:~
> $ scp -r $HBASE_HOME hduser@Slave3:~
所有 Slave nodes 都要做以下的步驟：
> $ sudo mv hbase /usr/local
> $ sudo chown -R hduser:hadoop /usr/local/hbase
> $ sudo chmod +x -R /usr/local/hbase
→ 將以下的資訊附加到 ~/.bashrc 與 ~/.profile 檔案末端：
export HBASE_HOME=/usr/local/hbase
讓新設定生效：
> $ source ~/.bashrc
> $ source ~/.profile
> $ update-alternatives --config java  # 尋找 java 在哪
( /usr/lib/jvm/java-7-openjdk-i386 )
> $ vim $HBASE_HOME/conf/hbase-env.sh  # 修改 JAVA_HOME 路徑
所有 node 的 hbase 格式化：( 每個 node 都要執行 )
> $ rm -rf $HBASE_HOME/logs/*  # 清空記錄檔
> $ rm -rf ~/hadoop/hbase-tmp/*  # 清空暫存檔
> $ rm -rf ~/hadoop/zookeeper/*
< 執行 Hadoop >

> $ hdfs dfsadmin -safemode leave  # Off the Safe mode of namenode
> $ start-dfs.sh
> $ start-yarn.sh