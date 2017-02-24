## �]�w�v��
- ������ root �ϥΪ�

$ su �V

- �ϥ�visudo �s���v��

$ visudo 

- ����sudo �v�� (��99��B)

hadoop	ALL=(ALL)	ALL

## Java �w��

### �����ª�Java
- yum -y remove java-*

### �U���Φw��Java

- https://mirror.its.sfu.ca/mirror/CentOS-Third-Party/NSG/common/x86_64/jdk-8u102-linux-x64.rpm

- sudo rpm -ivh jdk-8u102-linux-x64.rpm

### ��w�˥D���W�إ߳n�s��

- ln -s /usr/java/jdk1.8.0_102 /usr/java/java

### �]�wHadoop

- wget http://ftp.tc.edu.tw/pub/Apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz

- tar -zxvf hadoop-2.7.3.tar.gz


### �NHadoop 2.7.3 �h���� /usr/local
- sudo mv hadoop-2.7.3 /usr/local/hadoop

### �s��.bashrc
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

### ��s�ܼ�
$ source ~/.bashrc

### ���լO�_�i�H�L�K�X�n�J
- ssh localhost

### �ק�/etc/ssh/sshd_config
- sudo vi /etc/ssh/sshd_config
- �NPasswordAuthentication?�ܧ�no
- sudo service sshd restart

### �]�m�L�K�X�n�J
- ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
- cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
- chmod 700 ~/.ssh
- chmod 600  ~/.ssh/authorized_keys

### �ק�]�w��
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

### �榡��HDFS
- hdfs namenode -format

### �ҥ�HDFS
- start-yarn.sh

