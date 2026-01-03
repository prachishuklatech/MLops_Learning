🚀 Apache Kafka with Docker & Python (Beginner-Friendly Lab)

This repository demonstrates how to set up Apache Kafka using Docker Compose and interact with it using Python Producer and Consumer scripts.

The goal of this lab is to understand real-time data streaming, producer–consumer architecture, and how Kafka acts as a reliable middleman between systems — a foundational concept in MLOps and data engineering.

🧠 What You’ll Learn

By completing this lab, you will learn how to:

Set up Zookeeper and Kafka using Docker Compose

Create, list, and describe Kafka topics

Write Python Kafka Producer & Consumer scripts

Send and receive real-time messages

Shut down Kafka services cleanly

Understand Kafka’s role in scalable ML systems

🛠️ Tech Stack Used

Apache Kafka

Docker & Docker Compose

Python 3

kafka-python / kafka-python-ng

Ubuntu 24.04

VS Code

📂 Project Structure
.
├── docker-compose.yml
├── python-kafka-producer.py
├── python-kafka-consumer.py
├── kafka_venv/
└── README.md

⚙️ Environment Setup (Ubuntu 24.04)
1️⃣ Update system packages
sudo apt update

2️⃣ Install Python, pip, and virtual environment tools
sudo apt install -y python3-pip python3-venv

3️⃣ Create and activate virtual environment
python3 -m venv kafka_venv
source kafka_venv/bin/activate

4️⃣ Install Kafka Python libraries
pip install kafka-python kafka-python-ng


⚠️ Ensure the virtual environment is activated before running scripts.

🐳 Kafka Setup Using Docker Compose
Create docker-compose.yml
version: '3'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:7.6.6
    container_name: admin-zookeeper-1
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - "2181:2181"

  kafka:
    image: confluentinc/cp-kafka:7.6.6
    container_name: admin-kafka-1
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS: 0

Start Kafka Services
docker compose up -d


Verify containers are running:

docker ps

📌 Kafka Topic Management
Create a topic
docker exec admin-kafka-1 kafka-topics \
  --create \
  --topic sample-topic \
  --bootstrap-server localhost:9092 \
  --partitions 1 \
  --replication-factor 1

List topics
docker exec admin-kafka-1 kafka-topics \
  --list \
  --bootstrap-server localhost:9092

Describe topic
docker exec admin-kafka-1 kafka-topics \
  --describe \
  --topic sample-topic \
  --bootstrap-server localhost:9092

🧪 Python Kafka Consumer

The consumer continuously listens to messages from Kafka and prints them in real time.

Run the consumer:

python python-kafka-consumer.py


Run the producer in another terminal to send messages.

🧠 Why Kafka Matters (MLOps Perspective)

Kafka is widely used in production ML systems to:

Stream real-time data to ML models

Decouple data ingestion from model inference

Handle high-throughput and fault-tolerant pipelines

Power feature stores and online predictions

Strong ML systems start with strong data pipelines.

🧹 Clean Shutdown
docker compose down

📌 Conclusion

This lab builds a strong foundation for understanding real-time systems used in modern MLOps and distributed architectures.
