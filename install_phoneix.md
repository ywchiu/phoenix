### 下載Phoenix
- wget http://apache.stu.edu.tw/phoenix/apache-phoenix-4.9.0-HBase-1.2/bin/apache-phoenix-4.9.0-HBase-1.2-bin.tar.gz
- tar -zxvf apache-phoenix-4.9.0-HBase-1.2-bin.tar.gz

### 啟用phoenix
- cp apache-phoenix-4.9.0-HBase-1.2-bin/phoenix-4.9.0-HBase-1.2-server.jar $HBASE_HOME/lib
- stop-hbase.sh
- start-hbase.sh

### 啟用Squirrel
java -jar squirrel-sql-3.7.1-standard.jar 