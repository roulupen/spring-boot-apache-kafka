# Spring boot Apache Kafka

## Setting up Kafka and zookeeper in local system

For setting zookeeper and Kafka in local system you can refer below article:
https://dzone.com/articles/running-apache-kafka-on-windows-os

Once Kafka server is running you can interact with Kafka server with following commads:

- Runnung zoopkeeper service:
  - zkserver

- Running Kafka Service:
  - \bin\windows\kafka-server-start.bat .\config\server.properties

- To create a topic in Kafka(Need only once, subsequent time we can simply resue it):
  - kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic [Topic Name]

- Kafka producer from command line:
  - kafka-console-producer.bat --broker-list localhost:9092 --topic [Topic Name]

- Kafka consumer from command line(topic Kafka_demo):
  - kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic [Topic Name]

- List out all topics present in your Kafka server:
  - kafka-topics.bat --list --zookeeper localhost:2181

- Read messages from the begining:
  - kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic [Topic Name] --from-begin

- Delete a topic:
  - kafka-run-class.bat kafka.admin.TopicCommand --delete --topic [Topic Name] --zookeeper localhost:2181

## Apache Kafka producer using Spring boot:
https://github.com/roulupen/spring-boot-kafka-producer

First setup Apache Kafka in your local machine using above mentioned steps and create Kafka topics Kafka_Demo and Kafka_Demo_User. Kafka_Demo topic used for publishing String messages and Kafka_Demo_User topic used for publicing JSON message of model User.

This is the repo for producer: https://github.com/roulupen/spring-boot-kafka-producer.git 

This module has two end points:
- http://localhost:8081/kafka/publish/[MessageContent] , this is a GET request and pass the message content in the URL and it'll publish the message in "Kafka_Demo" topic.
- http://localhost:8081/kafka/publish , this is a POST resquest and we need the pass the JSON string in the request body and content type = JSON.
```
        {
            "name" : "Upendra",
            "dept" : "Home",
            "salary": 12000
        }
```

Reference: https://www.youtube.com/watch?v=NjHYWEV_E_o 

## Apache Kafka consumer using Spring boot:
https://github.com/roulupen/spring-boot-kafka-consumer 

Once the producer application pblishes the messages into different Kafka topics the consumer application need to read the messages from the corresponding topics.

Earlier we created two topics, Kafka_Demo(for plain text message) and Kafka_Demo_User(for User POJO). So, in consumer module I have created two listener to read from two different topics. You can find the detail code in below git repo: https://github.com/roulupen/spring-boot-kafka-consumer.git 

So, finally whatever the messages the producer will produce you can find those messages in the cosumer console.

Reference: https://www.youtube.com/watch?v=IncG0_XSSBg 


Other references:
- https://www.infoq.com/articles/apache-kafka/

