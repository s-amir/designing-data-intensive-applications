# designing-data-intensive-applications
__________

This repository contains key insights and notes from Designing Data-Intensive Applications by Martin Kleppmann. The book explores the fundamental principles behind scalable, reliable, and maintainable data systems.

Overview

Modern applications are increasingly data-intensive rather than compute-intensive. The book explores how to design systems that efficiently manage large-scale data while ensuring reliability and maintainability.

Key Concepts

## 1. Data-Intensive vs. Compute-Intensive Applications

CPU is rarely the bottleneck; instead, challenges arise from data volume, complexity, and speed.

Systems are built using a combination of:

### Databases (e.g., PostgreSQL, MongoDB)

### Caches (e.g., Redis, Memcached)

### Search Indexes (e.g., Elasticsearch, Apache Solr)

### Stream Processing Systems (e.g., Apache Kafka, Flink)

### Batch Processing Systems (e.g., Apache Hadoop, Spark)

## 2. Design Goals of Data Systems

A well-designed data system should focus on three core principles:

### Reliability

Ensures the system continues functioning correctly despite faults.

Handling Hardware Failures: Use redundancy (RAID, backups, multi-region deployment).

Mitigating Software Bugs: Implement process isolation, self-checking mechanisms, and failure simulations.

Preventing Human Errors: Design safe defaults, enable rollbacks, and use monitoring tools.

### Scalability

Ensures the system can handle increasing amounts of data and traffic.

Partitioning (Sharding): Splitting data across multiple nodes.

Replication: Keeping multiple copies of data for fault tolerance.

Indexing & Caching: Improving query performance.

### Maintainability

Ensures the system remains easy to modify and extend over time.

Clear Abstractions & APIs: Reduces complexity.

Automation: Prevents human errors.

Observability: Logging and monitoring for troubleshooting.




