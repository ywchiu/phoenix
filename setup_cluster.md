### �ק�t�m���G�n�J Master �q���ӭק�]�w >

regionservers # �]�w regionservers
backup-masters # �]�w backup master
hbase-site.xml # �]�w Configure ZooKeeper
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
���U�ӡA�N���s���t�m�A�ƻs��Ҧ�nodes�G
> $ scp -r $HBASE_HOME hduser@Slave1:~
> $ scp -r $HBASE_HOME hduser@Slave2:~
> $ scp -r $HBASE_HOME hduser@Slave3:~
�Ҧ� Slave nodes ���n���H�U���B�J�G
> $ sudo mv hbase /usr/local
> $ sudo chown -R hduser:hadoop /usr/local/hbase
> $ sudo chmod +x -R /usr/local/hbase
�� �N�H�U����T���[�� ~/.bashrc �P ~/.profile �ɮץ��ݡG
export HBASE_HOME=/usr/local/hbase
���s�]�w�ͮġG
> $ source ~/.bashrc
> $ source ~/.profile
> $ update-alternatives --config java  # �M�� java �b��
( /usr/lib/jvm/java-7-openjdk-i386 )
> $ vim $HBASE_HOME/conf/hbase-env.sh  # �ק� JAVA_HOME ���|
�Ҧ� node �� hbase �榡�ơG( �C�� node ���n���� )
> $ rm -rf $HBASE_HOME/logs/*  # �M�ŰO����
> $ rm -rf ~/hadoop/hbase-tmp/*  # �M�żȦs��
> $ rm -rf ~/hadoop/zookeeper/*
< ���� Hadoop >

> $ hdfs dfsadmin -safemode leave  # Off the Safe mode of namenode
> $ start-dfs.sh
> $ start-yarn.sh