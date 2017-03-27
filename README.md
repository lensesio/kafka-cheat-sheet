# kafka-cheat-sheet

# TOPICS

Creating a New Topic
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --create --topic my-topic --replication-factor 2 --partitions 8
```
Adding Partitions
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --alter --topic my-topic --partitions 16
```
Deleting a Topic
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --delete --topic my-topic
```
Listing All Topics in a Cluster
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --list
```
Describing Topic Details
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --describe
```
Show Under-replicated Partitions
```
kafka-topics --zookeeper localhost:2181/kafka-cluster --describe --under-replicated-partitions
```

# CONSUMERS
List Consumers
```
kafka-consumer-groups --zookeeper localhost:2181 --list
```

```
kafka-consumer-groups --new-consumer --bootstrap-server kafka1.example.com:9092/kafka-cluster --list
```
Describe Groups
```
kafka-consumer-groups --zookeeper localhost:2181/kafka-cluster --describe --group testgroup
```
Delete Group
```
kafka-consumer-groups --zookeeper localhost:2181/kafka-cluster --delete --group testgroup
```
Delete offsets from Group
```
kafka-consumer-groups --zookeeper localhost:2181/kafka-cluster --delete --group testgroup --topic my-topic
```
Export offsets
```
kafka-run-class kafka.tools.ExportZkOffsets --zkconnect localhost:2181/kafka-cluster --group testgroup --output-file offsets
```
Import offsets [Stop Consumers First]
```
kafka-run-class kafka.tools.ImportZkOffsets --zkconnect localhost:2181/kafka-cluster --input-file offsets
```

# PRODUCER
Produce two messages to a topic named “my-topic”
```
kafka-console-producer --broker-list kafka1.example.com:9092,kafka2.example.com:9092 --topic my-topic
```
Consume a single topic
```
kafka-console-consumer --zookeeper localhost:2181/kafka-cluster --topic my-topic
```
Consume a single message from the offsets topic
```
kafka-console-consumer --zookeeper localhost:2181/kafka-cluster --topic __consumer_offsets --formatter 'kafka.coordinator.GroupMetadataManager$Off setsMessageFormatter' --max-messages 1
```

# CONFIG
Set the retention for the topic
```
kafka-configs --zookeeper localhost:2181/kafka-cluster --alter --entity-type topics --entity-name my-topic --add-config
retention.ms=3600000
``` 
Show all configuration overrides for a topic
```
kafka-configs --zookeeper localhost:2181/kafka-cluster --describe --entity-type topics --entity-name my-topic4 
```
Delete a configuration override for retention.ms for a topic 
```
kafka-configs --zookeeper localhost:2181/kafka-cluster --alter --entity-type topics --entity-name my-topic --delete-config retention.ms 
```
