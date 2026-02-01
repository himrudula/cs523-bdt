# CS523 Big Data Technologies Lab

This repository contains the Docker Compose configuration and necessary Windows utilities for the CS523 Big Data Technologies lab environment.

## Overview

The setup provides a complete Big Data stack running in Docker containers, including:
- **Hadoop (HDFS & YARN)**
- **Apache Hive** (with Postgres as Metastore)
- **Apache HBase**
- **Apache Spark**
- **Apache Kafka**
- **Apache Zookeeper**

## Project Structure

- `docker-compose.yml`: Defines the multi-container Docker application.
- `hadoop.dll` & `winutils.exe`: Required for running Hadoop/Spark components on Windows.
- `my_code/`: (Optional) This directory is mapped to `/opt/my_code` inside the main lab container for sharing files between your host and the container.

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running.
- (Windows users) Ensure your Docker is configured to use Linux containers (default).

## Getting Started

1. **Start the environment:**
   Open a terminal in the project root and run:
   ```bash
   docker-compose up -d
   ```

2. **Accessing the Lab Container:**
   To interact with the big data tools via the command line, exec into the `cs523bdt-lab` container:
   ```bash
   docker exec -it cs523bdt-lab /bin/bash
   ```

3. **Stopping the environment:**
   ```bash
   docker-compose down
   ```

## Web Interfaces

Once the containers are running, you can access the following UIs in your browser:

| Service | URL |
|---------|-----|
| HDFS NameNode | [http://localhost:9870](http://localhost:9870) |
| YARN Resource Manager | [http://localhost:8088](http://localhost:8088) |
| HBase Master | [http://localhost:16010](http://localhost:16010) |
| Spark History Server / Job UI | [http://localhost:4040](http://localhost:4040) |

## Connection Details

- **Hive JDBC:** `localhost:10000`
- **Kafka Broker:** `localhost:9092`
- **Zookeeper:** `localhost:2181`
- **Postgres (Hive Metastore):** `localhost:5432`

## Windows Specifics

If you are running Spark or Hadoop locally on your Windows machine (outside of Docker), you may need to:
1. Create a directory (e.g., `C:\hadoop\bin`).
2. Place `winutils.exe` and `hadoop.dll` into that `bin` directory.
3. Set the `HADOOP_HOME` environment variable to `C:\hadoop`.
4. Add `%HADOOP_HOME%\bin` to your system `PATH`.

## Notes

- The environment is configured with the `America/Chicago` timezone by default.
- Data in the Hive Metastore (Postgres) is persisted using a Docker volume named `hive_db_data`.
