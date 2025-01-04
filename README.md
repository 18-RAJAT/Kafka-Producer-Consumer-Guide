# Kafka Producer Consumer Guide

## Introduction and Prerequisites

This tutorial covers the Kafka producer and consumer workflow using the command-line interface (CLI). It is recommended to watch the previous video on Kafka components and architecture before proceeding.
---

![PC](https://github.com/user-attachments/assets/251b025a-889d-49cd-a068-8ddd1db24d98)


## Setting up Kafka Ecosystem

To set up the Kafka ecosystem, you need to start the Zookeeper (the manager for Kafka) and the Kafka server (broker). Use the following commands to start Zookeeper and the Kafka server:

```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

and

```bash
bin/kafka-server-start.sh config/server.properties
```

## Producer and Consumer Communication

Producers and consumers communicate via a topic. Topics require specifying the number of partitions and replication factors based on load requirements.

## Creating Topics

To create a topic, use the following command:

```bash
bin/kafka-topics.sh --create --topic <topic-name> --bootstrap-server localhost:9092 --partitions <num-partitions> --replication-factor <replication-factor>
```

To list existing topics, use:

```bash
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

To describe a topic, use:

```bash
bin/kafka-topics.sh --describe --topic <topic-name> --bootstrap-server localhost:9092
```

## Message Flow

Messages from the producer are distributed across partitions within a topic. Consumers read messages from these partitions.

## CLI Demonstrations

To start a producer via CLI, use:

```bash
bin/kafka-console-producer.sh --topic <topic-name> --bootstrap-server localhost:9092
```

To start a consumer via CLI, use:

```bash
bin/kafka-console-consumer.sh --topic <topic-name> --from-beginning --bootstrap-server localhost:9092
```

## Bulk Message Handling

To push bulk data (e.g., from a CSV file with 1,000 rows) to Kafka, you can use:

```bash
bin/kafka-console-producer.sh --topic <topic-name> --bootstrap-server localhost:9092 < /path/to/your/file.csv
```

## Partition Insights

The distribution of messages to partitions is managed by Kafka and is not manually controlled. Observations on message allocation across partitions can be made during testing.

## Confluent Kafka

Confluent Kafka provides an extended platform for working with Kafka, offering enhanced features and tools. Below are commands specific to Confluent Kafka:

To start Zookeeper and Kafka in Confluent Kafka:

```bash
confluent local services zookeeper start
confluent local services kafka start
```

To create a topic:

```bash
confluent local services kafka topic create <topic-name> --partitions <num-partitions> --replication-factor <replication-factor>
```

To list topics:

```bash
confluent local services kafka topic list
```

To produce messages:

```bash
confluent local services kafka produce <topic-name>
```

To consume messages:

```bash
confluent local services kafka consume <topic-name> --from-beginning
```

To stop services:

```bash
confluent local services stop
```

## Offset Explorer

Offset Explorer (formerly known as Kafka Tool) is a GUI application for managing and monitoring Apache Kafka. It allows users to browse topics, view consumer group offsets, and produce or consume messages via an interactive interface. Below are key features and steps to get started:

### Features

1. **Topic Browsing**: View existing topics, partitions, and configurations.
2. **Consumer Group Management**: Monitor consumer offsets and lag.
3. **Message Inspection**: Produce and consume messages in a user-friendly manner.
4. **Cluster Monitoring**: Visualize broker statuses and metrics.

### Getting Started

1. Download Offset Explorer from the official website.
2. Connect to your Kafka cluster by providing broker addresses.
3. Explore the topics, manage offsets, and monitor the health of your cluster through the intuitive UI.

## Conclusion

This guide provides a comprehensive overview of the Kafka producer and consumer workflow using the CLI and Confluent Kafka commands, as well as an introduction to Offset Explorer for enhanced Kafka management. Follow the commands to set up your Kafka environment and start producing and consuming messages effectively.
