### kafka的安装

kafka依赖于ZooKeeper,所以在运行kafka之前需要先部署ZooKeeper集群，ZooKeeper集群部署方式分为两种,一种是单独部署(推荐),另外一种是使用kafka自带的。
这里我们默认已经部署好了ZooKeeper集群

- 下载kafka(3台服务器)
```
cd /usr/local/src
wget  http://apache.opencas.org/kafka/2.1.0/kafka_2.11-2.1.0.tgz
tar -zxvf kafka_2.11-2.1.0.tgz
mv /usr/local/src/kafka_2.11-2.1.0  /usr/local/kafka
```
- 修改配置文件
```
主要关注：server.properties 这个文件即可
cd /usr/local/kafka
```
配置文件详情解释
```
broker.id=0  #当前机器在集群中的唯一标识，和zookeeper的myid性质一样
port=19092 #当前kafka对外提供服务的端口默认是9092
host.name=192.168.7.100 #这个参数默认是关闭的，在0.8.1有个bug，DNS解析问题，失败率的问题。
num.network.threads=3 #这个是borker进行网络处理的线程数
num.io.threads=8 #这个是borker进行I/O处理的线程数
log.dirs=/opt/kafka/kafkalogs/ #消息存放的目录，这个目录可以配置为“，”逗号分割的表达式，上面的num.io.threads要大于这个目录的个数这个目录，如果配置多个目录，新创建的topic他把消息持久化的地方是，当前以逗号分割的目录中，那个分区数最少就放那一个
socket.send.buffer.bytes=102400 #发送缓冲区buffer大小，数据不是一下子就发送的，先回存储到缓冲区了到达一定的大小后在发送，能提高性能
socket.receive.buffer.bytes=102400 #kafka接收缓冲区大小，当数据到达一定大小后在序列化到磁盘
socket.request.max.bytes=104857600 #这个参数是向kafka请求消息或者向kafka发送消息的请请求的最大数，这个值不能超过java的堆栈大小
num.partitions=1 #默认的分区数，一个topic默认1个分区数
log.retention.hours=168 #默认消息的最大持久化时间，168小时，7天
message.max.byte=5242880  #消息保存的最大值5M
default.replication.factor=2  #kafka保存消息的副本数，如果一个副本失效了，另一个还可以继续提供服务
replica.fetch.max.bytes=5242880  #取消息的最大直接数
log.segment.bytes=1073741824 #这个参数是：因为kafka的消息是以追加的形式落地到文件，当超过这个值的时候，kafka会新起一个文件
log.retention.check.interval.ms=300000 #每隔300000毫秒去检查上面配置的log失效时间（log.retention.hours=168 ），到目录查看是否有过期的消息如果有，删除
log.cleaner.enable=false #是否启用log压缩，一般不用启用，启用的话可以提高性能
zookeeper.connect=192.168.7.100:12181,192.168.7.101:12181,192.168.7.107:1218 #设置zookeeper的连接端口
```
实际配置参数如下(具体根据实际情况做修改)
```
broker.id=0
#listeners=PLAINTEXT://:9092 -----》注释掉修改为如下
port=9092
host.name=192.168.94.130  (每台服务器地址需要单独修改)
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
log.dirs=/tmp/kafka-logs
num.partitions=1
num.recovery.threads.per.data.dir=1
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
zookeeper.connect=192.168.94.130:12181,192.168.94.131:12181,192.168.94.132:12181
zookeeper.connection.timeout.ms=6000
group.initial.rebalance.delay.ms=0
```

- 启动(3台服务器上执行)

```
/usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/server.properties
```

- 查看

```
[root@localhost ~]# jps
1745 QuorumPeerMain
3564 Jps
3501 Kafka
```
这样就安装完成了

### kafka的基本使用

- 创建一个名为“test”的Topic，只有一个分区和一个备份

```
 bin/kafka-topics.sh --create --zookeeper 192.168.94.130:12181，192.168.94.131:12181，192.168.94.132:12181 --replication-factor 1 --partitions 1 --topic test
```
- 查看已创建的topic信息：
```
./kafka-topics.sh --list --zookeeper 192.168.94.130:12181,192.168.94.131:12181,192.168.94.132:12181
```
测试发送消息

`
```
生产者
./kafka-console-producer.sh --broker-list 192.168.94.130:9092,192.168.94.131:9092,192.168.94.132:9092 --topic shuaige

消费者
./kafka-console-consumer.sh --bootstrap-server 192.168.94.132:9092,192.168.94.131:9092,192.168.94.130:9092 --topic shuaige  --from-beginning
```
查看不同topic下的broker信息
```

./kafka-topics.sh --describe --zookeeper 192.168.94.130:12181,192.168.94.131:12181,192.168.94.132:12181 --topic first
```
```
[root@localhost bin]# ./kafka-topics.sh --describe --zookeeper 192.168.94.130:12181,192.168.94.131:12181,192.168.94.132:12181--topic first
Topic:first     PartitionCount:1        ReplicationFactor:3     Configs:
        Topic: first    Partition: 0    Leader: 1       Replicas: 1,2,3 Isr: 1,2,3
[root@localhost bin]# ./kafka-topics.sh --describe --zookeeper 192.168.94.130:12181,192.168.94.131:12181,192.168.94.132:12181 --topic second
Topic:second    PartitionCount:2        ReplicationFactor:3     Configs:
        Topic: second   Partition: 0    Leader: 3       Replicas: 3,1,2 Isr: 3,2,1
        Topic: second   Partition: 1    Leader: 1       Replicas: 1,2,3 Isr: 1,2,3
```

相关信息解释

是输出解释。第一行给出了各个分区的概况，分区有几个就有几行分区详细信息介绍。（我创建了两个topic，一个是first，只有一个分区；一个是second，两个分区）
- Leader：是负责当前分区的所有读写请求。每个节点都将领导一个随机选择的分区。
- Replicas ：是节点列表，复制分区日志，不管他们是不是Leader或者不管它们是否还活着。
-  Isr：是in-sync的集合。这是Replicas列表当前还活着的子集。 

相关日志说明

server.log #kafka的运行日志
state-change.log  #kafka他是用zookeeper来保存状态，所以他可能会进行切换，切换的日志就保存在这里
controller.log #kafka选择一个节点作为“controller”,当发现有节点down掉的时候它负责在游泳分区的所有节点中选择新的leader,这使得Kafka可以批量的高效的管理所有分区节点的主从关系。如果controller down掉了，活着的节点中的一个会备切换为新的controller.

常见错误：
在消费或者在生产者地方报错
`
```
[root@localhost bin]# ./kafka-console-consumer.sh --bootstrap-server 192.168.94.130:9092 --topic shuaige --from-beginning
[2019-04-06 23:36:40,431] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 10 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:40,557] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 11 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:40,682] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 12 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:40,805] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 13 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:40,936] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 14 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:41,064] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 15 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:41,198] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 16 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:41,424] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 19 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:42,109] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 31 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:42,236] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 32 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:42,356] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 33 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:42,727] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 41 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:42,954] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 44 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:43,080] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 45 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:43,214] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 46 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:43,340] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 47 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:43,455] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 48 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:43,984] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 60 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:44,108] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 61 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:44,233] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with correlation id 62 : {shuaige=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2019-04-06 23:36:44,574] WARN [Consumer clientId=consumer-1, groupId=console-consumer-20606] Error while fetching metadata with c
```
解决办法
```
经过反复测试验证环境配置信息，最终参考了他人的经验，是kafka的server.properties的配置错误。主要是下面的内容配置有问题：listeners=PLAINTEXT://:9092
将这句注释掉，然后在配置文件中添加下面的两行配置，
指明当前broker的地址：port=9092
host.name=192.168.94.130 #依据具体的服务器，配置相应的服务器的IP地址即可。
(3台服务器都需要修改)
```
