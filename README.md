# Replication
PostgreSQL Streaming Replication Cluster with Docker Compose and HAProxy

This repository demonstrates how to set up a PostgreSQL streaming replication cluster using Docker Compose and HAProxy for load balancing. It includes one primary PostgreSQL node and two replicas for high availability and scalability.

Architecture

Primary Node: Handles all write operations.

Replica Nodes: Synchronize with the primary node and handle read operations.

HAProxy: Distributes incoming connections between the primary and replicas.

etcd: Provides coordination for the cluster.

Services Overview

postgres_primary: The primary PostgreSQL instance.

postgres_replica1 and postgres_replica2: Replica instances using streaming replication.

etcd: Coordination service.

haproxy: Load balancer to route traffic to the primary and replicas.

Prerequisites

Docker and Docker Compose installed on your machine.

Navicat (or any other PostgreSQL client) for connecting to the cluster.

Setup Instructions
 1) Clone the repository
      git clone https://github.com/MohammadMehradM1382/replication.git
      cd postgres-replication-cluster

 2) Create necessary directories
      mkdir -p primary_data replica1_data replica2_data primary_config replica1_config replica2_config
    
 3) Review and modify configuration files if needed
     primary_config/postgresql.conf: Configuration for the primary node.

     primary_config/pg_hba.conf: Access control settings.

     replica1_config/recovery.signal and replica2_config/recovery.signal: Standby mode indicators.

     haproxy.cfg: Load balancer configuration.

 4)start the cluster

     docker-compose up -d

 This will start all services, including the primary PostgreSQL node, two replicas, etcd, and HAProxy.
 
5) Connect to the Cluster
    Use Navicat or any PostgreSQL client to connect to HAProxy:

      Host: localhost

      Port: 5000

      Username: postgres

      Password: postgres_pass

      Database: mydb

 6) Verify Replication
     Insert data into the primary node and verify that it is replicated to the replicas.

      Example SQL command:

      INSERT INTO test_table (id, name) VALUES (1, 'Test Data');
    
       SELECT * FROM test_table;
    
 8) Simulate Failover
    To simulate a failover, stop the primary node:

        docker stop postgres_primary

        HAProxy will automatically reroute traffic to the replicas.
 9) cleanup(optional)

      To stop and remove all containers:

      docker-compose down

Notes

Ensure that your pg_hba.conf and postgresql.conf files are properly configured for replication.

Monitor replication status using pg_stat_replication on the primary node.


