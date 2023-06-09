# Kafka Overview
Apache Kafka Overview

### What is Apache Kafka

Apache Kafka is an open-source distributed streaming platform that is used to build real-time data pipelines and streaming applications. Kafka allows you to publish and subscribe to streams of records, similar to a message queue or enterprise messaging system.

Kafka is designed to be highly scalable, fault-tolerant, and durable. It is also very fast, capable of handling thousands of messages per second. 

#### What are Core components

The core components of Kafka are:

- Kafka brokers: these store and manage the streams of records.
- Kafka clients: these are used to produce and consume the records.

![image](https://github.com/santoshjoshi/kafka-interview-questions/assets/614170/6a9a4520-bf5d-4234-a4ee-1bf487242a9d)


### What are topics and partitions 

#### Topics
In Apache Kafka, a topic is a category or feed name to which messages are published. Topics are partitioned and distributed across the Kafka cluster for scalability and fault tolerance. Each partition of a topic is replicated across multiple brokers for redundancy.

#### Partitions

Partitions are the units of parallelism in Kafka. They allow the topic to be split into multiple smaller, more manageable segments. A partition is an ordered, immutable sequence of records that acts as a log. Messages in a partition are assigned a unique offset, which is used to identify their position within the partition.

When a producer publishes a message to a Kafka topic, the message is assigned to a partition based on a configurable partitioning strategy. The partition to which a message is assigned depends on factors such as the key of the message, the number of partitions in the topic, and the load balancing of the brokers.

Consumers can read messages from one or more partitions of a topic, in parallel. Each consumer reads from a unique offset in a partition.

Below is a diagram showing the relationship between topics and partitions in Kafka:
![image](https://github.com/santoshjoshi/kafka-interview-questions/assets/614170/9be2f557-3d54-46af-a44c-17a37bdffdc3)


#### What is a consumer group

* A consumer group is a set of related consumers
* Consumers from same group cannot read from same topic's partion.
* Consumers within a consumer group use GroupCordinator and ConsumerCordinator to assign a partion to a consumer. Each consumer get a "fair share” of partion
* Consumer group maintains its offset per topic partition.
* If there are more consumers then partitions, the extra consumers remain idle until some consumer dies.

![image](https://github.com/santoshjoshi/kafka-interview-questions/assets/614170/916947e5-f1b0-4b4b-9549-936bc7829488)


4. How do you create consumer groups

#### What is an offset
An offset is a unique identifier assigned to each message within a partition of a Kafka topic. 
- It represents the position of a message in the log of a partition.
- It tracks progress of consumers 
- whenever a nes message comes the offset is increased by 1

Some important characteristics are :

![image](https://github.com/santoshjoshi/kafka-interview-questions/assets/614170/ff5a3f73-98e1-48eb-9a38-265fcf5da098)

7. What are the different ways to commit an offset?
8. Does Kafka provides ordering guarantees? 

#### How offsets are stored in Kafka

Kafka stores offset in an internal topic( **__consumer_offsets** ). The offset is generally a key value pair where key is **<TOPIC,PARTITION,CONSUMER_GROUP_ID>** and the value is **offset**

#### What is the importance of __consumer_offsets topic

Offset is basically a pointer that specifies till what position the data has been consumed or produced for a given topic and partition. All Kafka offsets are stored on an internal topic named **__consumer_offsets** inside Kafka’s cluster. 
Offsets are committed by consumers to kafka cluster using auto-commit or by committing manually on code. The commit is analogous as relational database commits.

#### Can two consumers consume from the same topic?

It depends on the Group Id. As long as the consumers belong to different Group Id they can consume from the same topic. In other words, A message within the topic is consumed by only one consumer in a consumer group. In order to process a message by multiple consumers, we need to place it in a different consumer group.


9. What is the benefit of partitioning?

###  What is backpressure?

 The producer generally generates data and sends it to the consumer for processing. However, due to various factors such as limited resources or slower processing capabilities of the consumer, it may not be able to keep up with the rate of data production. To adderess this backpressure comes.
 
 When the consumer becomes overwhelmed or needs to slow down its processing, it sends a backpressure signal to the producer indicating its current capacity or readiness to receive data.
 
 Based on this signal, the producer adjusts its data production rate accordingly. It may slow down, pause, or adjust the volume of data it sends to the consumer until the backpressure signal is lifted.

### Kafka Monitoring
1. How are you Monitoring Apache Kafka? Have you used Kafka Manager
2. Kafka exposes metrics are you using it or plotting it somewhere if yes the how?


### Kafka Internals
1. How Kafka stores its data.
   https://thehoard.blog/how-kafkas-storage-internals-work-3a29b02e026
2. Why is Kafka So Fast
   https://www.freecodecamp.org/news/what-makes-apache-kafka-so-fast-a8d4f94ab145/
3. What is Zero copy approach
4. What is the anatomy of a Kafka Message or What does a kafka message in a topic contains.

### Kafka Topology
1. Explain the topology of Apache KafkaHow many nodes of Apache Kafka
2. How many Zookeeper Instances
3. What is the data scale? How much data are you managing using
4. Kafka How Many Topics are there 
5. How are partition look like. How many partitions per topic.
6. How much data are you get per minute/day?
7. What are the message inflow and outflow rate?
8. What is the bandwidth usage?
9. What is disk space usage?

### Kafka Topics
* Explain the anatomy of topic
* Topics. 
    * Compression
    * Partitions
    * Offsets
    * Log 
    * Log Segments
    * Log compaction

### Kafka Availability
1. What if a Kafka node dies out. Is there any monitoring in place. How much time would it take to find out a missing node?
2. How are you replacing a Kafka node in production? How much time does it take to replace a Kafka node?
3. Kafka needs Zookeeper. So if a Zookeeper node dies out,  How are you replacing it and how is Kafka managing. Are you stopping Kafka and replace Zookeeper Ip and restarting.
4. What happens to the producer when a broker is down. How are you handling this in Producer?
5. What happens when a broker is down and no ISR is available
6. What is the average downtime in a month

#### How to increase replication factor for a topic

Increasing replication is a 4 step process that includes

1. Check existing partition assignment
2. Create a custom reassignment plan ( a JSON file)
3. Do the reassignment process
4. Verify the assignments

Have documented some of the things here 
[Increasing Replicas](https://whiteboardtalks.com/how-to-increase-replication-factor-for-a-kafka-topic/)


### Kafka Producer Configuration or Tuning Kafka Producer

When creating a Kafka Producer, on need to configure of should know about these onse.

- **Compression:**
        compression.type: This configuration determines the compression codec to be used for compressing messages sent by the producer. Supported options include "none" (no compression), "gzip", "snappy", "lz4", and "zstd". Compression can help reduce network bandwidth and storage requirements for Kafka messages.

- **Batch Size:**
        batch.size: This configuration specifies the maximum size (in bytes) of the message batch that the producer will send to a Kafka broker in a single request. Larger batch sizes generally improve throughput by reducing the overhead of network requests.

- **Sync or Async:**
        acks: This configuration determines the level of acknowledgment expected from Kafka brokers after producing a message. Options include "all" (leader and replicas acknowledge), "1" (leader acknowledges), and "0" (no acknowledgment). Choosing synchronous or asynchronous mode affects the behavior of the producer.

- **linger.ms:**
        linger.ms: This configuration introduces a delay (in milliseconds) in the producer to allow more messages to accumulate in the batch before sending them. It helps increase batching efficiency by reducing the number of smaller requests.

- **retry.backoff.ms:**
        retry.backoff.ms: This configuration specifies the time (in milliseconds) the producer waits before retrying a failed message send attempt. It is used when a transient error occurs, such as a network issue or a Kafka broker being temporarily unavailable.

- **max.in.flight.requests.per.connection:**
        max.in.flight.requests.per.connection: This configuration sets the maximum number of unacknowledged requests the producer can have outstanding before it stops sending additional requests. It allows controlling the maximum level of parallelism while maintaining the order of messages.

### Kafka Manager
1. What is an in-sync replica and how it differs from normal replica
2. What is broker Skew and broker spread
3. What is the purge strategy
4. How Kafka manages replication. What is your replication strategy?

### Kafka provisioning & Installation
1. How are you installing Kafka? 
2. How are you provisioning Kafka in cloud? What tools are you using, packer, terraform, anisble... and How
3. How often do you make changes to prod Kafka?
4. Are you using Docker Is Zookeeper bundled in the same container?

#### How are you monitoring Kafka?

Monitoring kafka may involves

* Broker Monitoring
    * Infra Monitoring
        * Disk
        * CPU
        * Memory
        * Network/ Bandwidt 
    * Producer Monitoring
    * Consumer Monitoring
        * Consumer Offset Monitoring or Consumer Group Latency Monitoring

### Kafka & Zookeeper Backup and Restore
* Are you backing up Kafka’s data? Are you backing up Kafka’s topic configurations
* Any Tools you have used for backing and restore of Kafka
    * Burry.sh  https://github.com/mhausenblas/burry.sh
    * https://jobs.zalando.com/tech/blog/backing-up-kafka-zookeeper/
    * Uses https://github.com/spredfast/kafka-connect-s3 to take the backup of a topic
    * https://medium.com/@Pinterest_Engineering/zookeeper-resilience-at-pinterest-adfd8acf2a6b
* Uses Exhibitor UI for backing up Zookeeper 
* Uses https://github.com/spredfast/kafka-connect-s3 to take backup of a topic 

### Kafka Broker Logging Configuration
1. How will you debug any issue with Kafka? What are various log files used by Kafka broker.

Originally Added To:  https://whiteboardtalks.com/
