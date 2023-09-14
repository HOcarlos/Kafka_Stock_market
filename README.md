# Kafka_Stock_market
A Kafka project that takes information from the Stock Market in real-time from a CSV and store it on S3 Bucket

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/1aaf0f66-403e-4e88-997a-fc14dd52d4cb)

## AMAZON EC2
First, I have to create an instance on EC2.
With that, I have a Linux environment that I can access directly from my local PC.
### ADD IMAGE ###

## KAFKA
With the Linux environment created I installed Kafka and initialized the Zookeeper and the Kafka Server with the below commands:

#### Start Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties
#### Start Kafka Server
bin/kafka-server-start.sh config/server.properties

#### OBS: Zookeeper is used in distributed systems to coordinate distributed processes and services (in this case, Kafka)

#### After that I created a topic called "topic_stock_market" with the command below:
bin/kafka-topics.sh --create --topic topic_stock_market --bootstrap-server xx.xxx.xxx.xxx:9092 --replication-factor 1 --partitions 1

#### started the Producer:
bin/kafka-console-producer.sh --topic topic_stock_market --bootstrap-server xx.xxx.xxx.xxx:9092

#### started the Consumer
bin/kafka-console-consumer.sh --topic topic_stock_market --bootstrap-server xx.xxx.xxx.xxx:9092

## PYTHON
In python I created two files, "KafkaProducer.ipynb" and "KafkaConsumer.ipynb".

### KafkaProducer.ipynb
I create a Kafka Producer, passing as parameter the EC2 IP.
Read from a CSV File called "IndexProcessed.csv"
