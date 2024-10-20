# Kafka and Zookeeper Setup with Node.js and KafkaJS

This guide walks through the steps to set up Zookeeper and Kafka using Docker, and demonstrates how to install and use Node.js with KafkaJS for producing and consuming messages.

## Prerequisites

- Docker installed on your machine.
- Node.js installed.
- Corepack for Yarn package management.

## Steps

### 1. Running Zookeeper

Zookeeper is required for managing and coordinating Kafka brokers. You can run Zookeeper using Docker with the following command:

```bash
docker run -p 2181:2181 zookeeper
```

This will start Zookeeper on port `2181`.

### 2. Running Kafka

Kafka depends on Zookeeper to function. Use the following command to start a Kafka broker. Replace `192.168.18.10` with your local machine's IP address.

```bash
docker run -p 9092:9092 \
  -e KAFKA_ZOOKEEPER_CONNECT=192.168.18.10:2181 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.18.10:9092 \
  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
  confluentinc/cp-kafka
```

Kafka will now be running on port `9092`.

### 3. Installing Node.js

Ensure Node.js is installed on your system. If not, download and install it from [Node.js official website](https://nodejs.org/).

### 4. Enabling Yarn with Corepack

Yarn is a fast, secure, and reliable package manager. To enable it, run the following commands:

```bash
corepack enable  # Enable Corepack to manage Yarn versions
corepack prepare yarn@stable --activate  # Activate Yarn at stable version
```

### 5. Initializing a Node.js Project

Initialize your Node.js project using Yarn:

```bash
yarn init  # Initializes a new Node.js project
```

This will create a `package.json` file for managing your project's dependencies.

### 6. Adding KafkaJS Library

KafkaJS is a modern client for Apache Kafka. Install it using Yarn:

```bash
yarn add kafkajs  # Add KafkaJS to your project
```

### 7. Running Kafka Admin with Yarn PnP (Plug-and-Play)

To run the Kafka admin script using Yarn's Plug-and-Play (PnP) system, execute:

```bash
yarn node admin.js  # Runs your admin.js script with Yarn's PnP
```

### 8. Running the Kafka Producer

To run the Kafka producer script (`producer.js`), use the following command:

```bash
yarn node producer.js  # Runs your producer.js script to produce messages to Kafka
```

Make sure your `producer.js` script is correctly set up to send messages to your Kafka topic.

### 9. Running the Kafka Consumer

To run the Kafka consumer script (`consumer.js`) for a specific consumer group (`user_grp-1`), use the following command:

```bash
yarn node consumer.js user_grp-1  # Runs your consumer.js script to consume messages from Kafka using group user_grp-1
```

Ensure that your `consumer.js` script is set up to subscribe to the appropriate topic and consume messages using KafkaJS.

---

You are now ready to work with Kafka in a Node.js environment using KafkaJS for both producing and consuming messages!
