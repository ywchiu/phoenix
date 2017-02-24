
### �w�� HBase ����

- wget http://apache.stu.edu.tw/hbase/1.2.4/hbase-1.2.4-src.tar.gz
- tar -zxvf hbase-1.2.4-bin.tar.gz
- sudo mv hbase-1.2.4 /usr/local/hbase
- sudo chown -R hadoop:hadoop /usr/local/hbase
- sudo chmod +x -R /usr/local/hbase

### �ק������ܼ� (vi ~/.bashrc)
- export HBASE_HOME=/usr/local/hbase
- export PATH=$PATH:$HBASE_HOME/bin

### �ק�hbase-env.sh
- vim $HBASE_HOME/conf/hbase-env.sh  # �ק� JAVA_HOME ���|

```
/usr/java/jdk1.8.0_102/
```

### �ק�]�w��
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

## �ҥ�HBase
- start-hbase.sh
