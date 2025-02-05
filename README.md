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
      git clone https://github.com/yourusername/postgres-replication-cluster.git
      cd postgres-replication-cluster

 2) Create necessary directories

      mkdir -p primary_data replica1_data replica2_data primary_config replica1_config replica2_config
    Review and modify configuration files if needed

