# Kafka_Stock_market
A Kafka project that takes information from the Stock Market in real-time from a CSV and stores it on S3 Bucket, and after that can be read from AWS Glue and Athena.

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/1aaf0f66-403e-4e88-997a-fc14dd52d4cb)

## AMAZON EC2
First, I have to create an instance on EC2.
With that, I have a Linux environment that I can access directly from my local PC.

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/910b8b5f-ca7f-4dcd-9345-9154e8f6ffa2)


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
In Python I created two files, "KafkaProducer.ipynb" and "KafkaConsumer.ipynb".

### KafkaProducer.ipynb
*I imported some libraries* 

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/aaf08f92-99a6-4b9e-90b9-e0567dc6aae7)

*I created a Kafka Producer to send the data to the topic, passing as a parameter the EC2 IP.*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/7a74d5a6-bc16-4c09-b277-63dfa276c12c)

*Read from a CSV File called "IndexProcessed.csv"*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/f9f5c603-266e-419b-9e36-00f96d63d0b0)

*I created a loop that will take the records from the CSV file and send them to the "topic_stock_market" topic*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/d01bbbee-8aa8-4c63-93ea-59a5185baa1b)

### KafkaConsumer.ipynb
*Imported some libraries*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/293113eb-1fef-4deb-aebe-3d371f4a153b)

*I created a Kafka Consumer to consume the data from the "topic_stock_market" topic*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/a57a81c9-32e1-4b7a-b496-ce4ad0716d07)

*Initialize the S3 library that will be responsible for receiving the data from Kafka Consumer.*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/bc930a72-e151-4e89-8d5a-091d1d61b10b)

*A loop that will take them from the consumer and send them to S3*

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/e2c4effb-e271-48df-b841-dbdae08ae4f8)

## AWS

### AWS S3
Was created as a S3 bucket and when the producer and the consumer are running the S3 will increase.

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/f5a7847b-bbcf-40d9-9160-5bf03e21ee89)

### AWS Glue
To read the information from S3 Bucket, transform the data and put the information on a database.
**CRAWLER

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/0f6af1f9-a9ca-42b3-9b2a-84a0dd3a1d34)

**DATABASE

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/97877bfe-26f0-4ee7-9922-7a15e8a57b11)

### AWS ATHENA
After the data is passed from the AWS Glue, we will read that data to AWS Athena, which is a tool to analyze data.

![image](https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/e494bb72-ec76-4e52-96ad-fe978f2dd7cc)

And with that, we have a real-time data analysis using Python, Kafka, and some services from AWS.

https://github.com/HOcarlos/Kafka_Stock_market/assets/46444726/5c753323-863a-4954-8072-cdc38c770d40



