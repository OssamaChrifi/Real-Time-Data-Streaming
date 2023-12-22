# Realtime Data Streaming Project

## Table of Contents
- [Introduction](#introduction)
- [System Architecture](#system-architecture)
- [Technologies](#technologies)
- [Getting Started](#getting-started)

## Introduction

This project serves as a comprehensive guide to building an end-to-end data engineering pipeline. It covers each stage from data ingestion to processing and finally to storage, utilizing a robust tech stack that includes Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra. Everything is containerized using Docker for ease of deployment and scalability.

## System Architecture

The project is designed with the following components:

- **Data Source**: We use `randomuser.me` API to generate random user data for our pipeline.
- **Apache Airflow**: Responsible for orchestrating the pipeline and storing fetched data in a PostgreSQL database.
- **Apache Kafka and Zookeeper**: Used for streaming data from PostgreSQL to the processing engine.
- **Control Center and Schema Registry**: Helps in monitoring and schema management of our Kafka streams.
- **Apache Spark**: For data processing with its master and worker nodes.
- **Cassandra**: Where the processed data will be stored.

## Technologies

- Apache Airflow
- Python
- Apache Kafka
- Apache Zookeeper
- Apache Spark
- Cassandra
- PostgreSQL
- Docker

## Getting Started

1. Clone the repository:
    ```bash
    git clone https://github.com/OssamaChrifi/Real-Time-Data-Streaming.git
    ```

2. Navigate to the project directory:
    ```bash
    cd path/to/project
    ```

3. Run Docker Compose to spin up the services:
    ```bash
    docker-compose up -d
    ```

4. check all container if it's running properly:
    ```bash
    docker-compose ps
    ```
If some service did not work check the logs :

    ```bash
    docker-compose logs <container_ID_or_name>
    ```
5. run spark for data process :

    ```bash
    spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.13:3.5.0,com.datastax.spark:spark-cassandra-connector_2.13:3.4.1 \
    --conf spark.sql.extensions=com.datastax.spark.connector.CassandraSparkExtensions \
    --master spark://localhost:7077 \
    spark-stream.py
    ```
6. run the stream with airflow with the url : http://localhost:8080

You can check the console to see if data it's correctly send to kafka in this url : http://localhost:9021/

7. look into cassandra if table it's correctly created and update :

    ```bash
    docker exec -it cassandra cqlsh -u cassandra -p cassandra localhost 9042 
    ```
    ```sql
    SELECT * FROM spark_streams.created_users;
    ``` 










