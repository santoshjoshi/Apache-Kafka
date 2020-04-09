# Kafka Interview Questions
Apache Kafka Interview Questions

### Kafka Basics

1. What is Apache Kafka
2. What are topics and partitions 
3. What are various components of Kafka
4. What is a consumer group
5. What is an offset
6. What are the different ways to commit an offset?

#### What is the importance of __consumer_offsets topic

Offset is basically a pointer that specifies till what position the data has been consumed or produced for a given topic and partition. All Kafka offsets are stored on an internal topic named **__consumer_offsets** inside Kafka’s cluster. 
Offsets are committed by consumers to kafka cluster using auto-commit or by committing manually on code. The commit is analogous as relational database commits.

8. Can two consumers consume from the same topic?
9. What is the benefit of partitioning?
10. What is backpressure?

### Kafka Monitoring
1. How are you Monitoring Apache Kafka? Have you used Kafka Manager
2. Kafka exposes metrics are you using it or plotting it somewhere if yes the how?

### Kafka Internals
1. How Kafka stores its data.
   https://thehoard.blog/how-kafkas-storage-internals-work-3a29b02e026
2. Why is Kafka So Fast
   https://www.freecodecamp.org/news/what-makes-apache-kafka-so-fast-a8d4f94ab145/
3. What is Zero copy approach

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
1. Explain the anatomy of topic
2. Topics
     Partitions
     Offsets
     Log 
     Log Segments
     Log compaction


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
1. Describe the producer configuration you need to take care for configuring Kafka Producer. 
   Compression
   Batch size
   Sync or Async
   linger.ms
   retry.backoff.ms
   max.in.flight.requests.per.connection
   Acks

### Kafka Manager
1. What is an in-sync replica and how it differs from normal replica
2. What is broker Skew and broker spread
3. What is the purge strategy
4. How Kafka manages replication. What is your replication strategy?

### Kafka provisioning & Installation
1. How are you installing Kafka? 
2. How are you provisioning Kafka in cloud?
    What tools are you using , packer, terraform, anisble…?
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
