## 設定權限
- 切換成 root 使用者

$ su –

- 使用visudo 編輯權限

$ visudo 

- 給予sudo 權限 (於99行處)

hadoop	ALL=(ALL)	ALL

## Java 安裝

### 移除舊的Java
- yum -y remove java-*

### 下載及安裝Java

- https://mirror.its.sfu.ca/mirror/CentOS-Third-Party/NSG/common/x86_64/jdk-8u102-linux-x64.rpm

- sudo rpm -ivh jdk-8u102-linux-x64.rpm

### 於安裝主機上建立軟連結

- ln -s /usr/java/jdk1.8.0_102 /usr/java/java

### 設定Hadoop

- wget http://ftp.tc.edu.tw/pub/Apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz

- tar -zxvf hadoop-2.7.3.tar.gz


### 將Hadoop 2.7.3 搬移到 /usr/local
- sudo mv hadoop-2.7.3 /usr/local/hadoop

### 編輯.bashrc
- $ vim ~/.bashrc
- export JAVA_HOME=/usr/java/jdk1.8.0_102/
- export PATH=$PATH:$JAVA_HOME
- export HADOOP_PREFIX=/usr/local/hadoop 
- export HADOOP_COMMON_HOME=$HADOOP_PREFIX 
- export HADOOP_HDFS_HOME=$HADOOP_PREFIX 
- export HADOOP_MAPRED_HOME=$HADOOP_PREFIX 
- export HADOOP_YARN_HOME=$HADOOP_PREFIX 
- export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_PREFIX/lib/native
- export HADOOP_OPTS="-Djava.library.path=$HADOOP_PREFIX/lib"
- export HADOOP_CONF_DIR=$HADOOP_PREFIX/etc/hadoop 
- export PATH=$PATH:$HADOOP_PREFIX/bin:$HADOOP_PREFIX/sbin

### 更新變數
$ source ~/.bashrc

### 嘗試是否可以無密碼登入
- ssh localhost

### 修改/etc/ssh/sshd_config
- sudo vi /etc/ssh/sshd_config
- 將PasswordAuthentication?變更為no
- sudo service sshd restart

### 設置無密碼登入
- ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
- cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
- chmod 700 ~/.ssh
- chmod 600  ~/.ssh/authorized_keys

### 修改設定檔
- vi hdfs-site.xml
```
 <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
```
 
- vi core-site.xml
```
 <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost</value>
  </property>
```

### 格式化HDFS
- hdfs namenode -format

### 啟用HDFS
- start-dfs.sh

