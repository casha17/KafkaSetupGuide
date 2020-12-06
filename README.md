# KafkaSetupGuide
A guide for setting up kafka and zookeeper on a cluster

# Zookeepr 

First ssh into the server and download zookeeper
```
mkdir zookeeper && cd zookeeper
wget "https://mirrors.dotsrc.org/apache/zookeeper/zookeeper-3.6.2/apache-zookeeper-3.6.2-bin.tar.gz"
```
Unpack and moove

```
tar -zxf apache-zookeeper-3.6.2-bin.tar.gz

sudo mv apache-zookeeper-3.6.2-bin /usr/local/zookeeper

cd /usr/local/zookeeper/

sudo mkdir -m 777 /var/lib/zookeeper

cd /var/lib/zookeeper/
nano myid

nano conf/zoo.cfg

tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
initLimit=20
syncLimit=5
server.1=node-master:2888:3888
server.2=node1:2888:3888
server.3=node2:2888:3888

mkdir -m 777 data

echo "1" > data/myid
```

# Kafka

``` 
wget "https://mirrors.dotsrc.org/apache/kafka/2.6.0/kafka_2.12-2.6.0.tgz"
tar -zxf kafka_2.12-2.6.0.tgz
rm -rf kkafka_2.12-2.6.0.tgz
sudo mv kafka_2.12-2.6.0 /usr/local/kafka
mkdir /tmp/kafka-logs
nano /usr/local/kafka/config/server.properties

/usr/local/kafka/bin/kafka-topics.sh --create --zookeeper node-master:2181,node1:2181,node2:2181 --replication-factor 3 --partitions 10 --topic twitterraw
``` 


