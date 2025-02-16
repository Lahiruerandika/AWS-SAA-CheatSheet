# Databases

## Choosing the Right Database

There are several databases on AWS to choose from. Below are some guiding questions to help select the best database for your product:

- Is the workload read-heavy, write-heavy, or balanced? What are the throughput needs? Will the throughput change, fluctuate, or require scaling over time?
- How much data will be stored, and for how long? Will the data size grow? What is the average size of an object in the database? How frequently are these objects accessed?
- Data durability: Should the data be stored for a short period (e.g., a week) or permanently? Will the database serve as a source of truth?
- What are the latency concerns?
- What is the data model? How will the data be queried? Will the data be structured, semi-structured, or unstructured?
- Do we need a strict schema or a flexible schema? Do we require reporting capabilities or advanced search functionality?
- What are the licensing costs? Can we switch to a cloud-native database such as Aurora or DynamoDB?

## Database Types on AWS

- **Relational Databases (RDBMS) - SQL/OLTP:** Amazon RDS, Aurora – Ideal for joins and normalized data.
- **NoSQL Databases:** DynamoDB, ElastiCache (key/value pairs), Neptune (graph-based), DocumentDB (JSON) – No joins, no SQL.
- **Object Storage:** S3 (large object storage) / Glacier (backups, archiving).
- **Data Warehouse - SQL Analytics/BI:** Redshift (OLAP), Athena.
- **Search Engines:** OpenSearch (formerly ElasticSearch) – Full-text search and unstructured searches.
- **Graph Databases:** Neptune – Best suited for relationship-based data.

## Amazon RDS

- Managed relational database service supporting PostgreSQL, MySQL, Oracle, and SQL Server.
- AWS provisions an EC2 instance behind the scenes with an EBS volume.
- Supports multi-AZ deployment and read replicas.
- Security: IAM, security groups, KMS, SSL.
- Backup, snapshot, and point-in-time restore functionalities.
- Managed and scheduled maintenance.
- Monitoring through CloudWatch.
- **Use cases:** Storing relational datasets, performing SQL queries, handling transactional inserts, deletes, and updates.

### RDS for Solutions Architects

- **Operations:** Small downtime during failovers, maintenance, and scaling. Restoring snapshots requires manual intervention.
- **Security:** AWS manages OS security; users configure KMS, SG, IAM policies, user authorization, and SSL.
- **Reliability:** Multi-AZ feature ensures failover support.
- **Performance:** Depends on EC2 instance type and EBS volume. Read replicas are available, but RDS does not auto-scale.
- **Cost:** Pay per hour based on provisioned EC2 and EBS usage.

## Amazon Aurora

- Fully managed, part of RDS, compatible with PostgreSQL and MySQL.
- Data is replicated six times across three Availability Zones.
- Auto-healing capabilities with auto-scaling read replicas (global replicas supported).
- **Serverless Aurora option available.**
- **Use cases:** Similar to RDS but with better performance, less maintenance, and higher flexibility at a slightly higher cost.

### Aurora for Solutions Architects

- **Operations:** Reduced manual operations, auto-scaling storage.
- **Security:** AWS manages OS security; users handle KMS, SG, IAM policies, and SSL.
- **Reliability:** Multi-AZ, highly available, serverless option.
- **Performance:** 5x faster performance compared to other RDS types, supports up to 15 read replicas.
- **Cost:** Pay per EC2 instance and storage usage; potentially lower cost than enterprise-grade databases like Oracle.

## Amazon ElastiCache

- Managed **Redis** or **Memcached**.
- In-memory data store with sub-millisecond latency.
- Requires EC2 instance provisioning.
- Supports clustering (Redis) and multi-AZ read replicas (sharding).
- Security: IAM, SG, KMS, Redis Auth.
- Backups, snapshots, and point-in-time restore (for Redis).
- **Use cases:** Key/value store, frequent reads, caching database queries, session data storage.

### ElastiCache for Solutions Architects

- **Operations:** Similar to RDS.
- **Security:** Same as RDS but lacks IAM policies (uses Redis Auth instead).
- **Reliability:** Clustering, multi-AZ support.
- **Performance:** Sub-millisecond latency, sharding.
- **Cost:** Pay per EC2 instance type and storage.

## Amazon DynamoDB

- Fully managed NoSQL database, proprietary to AWS.
- **Serverless**, auto-scaling, supports provisioned and on-demand capacity.
- Highly available (multi-AZ by default), supports **DynamoDB Accelerator (DAX)** for read caching.
- Security, authentication, and authorization managed through IAM.
- **Use cases:** Serverless apps, distributed serverless caching, real-time applications.

### DynamoDB for Solutions Architects

- **Operations:** Fully serverless, auto-scaling enabled.
- **Security:** IAM policies, KMS encryption, SSL in transit.
- **Reliability:** Multi-AZ, backup and restore.
- **Performance:** Single-digit millisecond latency, DAX caching.
- **Cost:** Pay per provisioned capacity and storage usage.

## Amazon S3

- Key/value object store.
- **Best for large objects, not small files.**
- Serverless, infinitely scalable (5TB max per object).
- Storage classes: **S3 Standard, S3 IA, One Zone IA, Glacier.**
- **Use cases:** Static file hosting, key-value storage, website hosting.

## Amazon Athena

- Fully **serverless** query engine with SQL capabilities.
- Queries data stored in **S3**.
- **Pay per query.**
- **Use cases:** Ad-hoc SQL queries on S3, log analysis.

## Amazon Redshift

- **OLAP (Analytical Processing)**, not OLTP.
- **10x performance improvement over traditional data warehouses.**
- Massively Parallel Processing (MPP), columnar storage.
- **Use cases:** BI tools (QuickSight, Tableau), big data analytics.

### Redshift Spectrum

- Queries **S3 data directly** without loading it into Redshift.
- Requires a running Redshift cluster.

## Amazon Neptune

- Fully managed **graph database**.
- **Use cases:** Relationship-based data, social networks, knowledge graphs.
- Supports point-in-time recovery, continuous backups.
- **Security:** IAM, KMS encryption, HTTPS.

## Amazon OpenSearch (Formerly ElasticSearch)

- **Used for full-text search, log analytics, and visualization.**
- **Integrations:** AWS Kinesis Data Firehose, AWS IoT, CloudWatch Logs.
- Security: IAM, KMS encryption, SSL, Cognito authentication.
- Comes with **Kibana** and **Logstash** (**ELK stack**).

### OpenSearch for Solutions Architects

- **Operations:** Similar to RDS.
- **Security:** IAM, VPC, KMS, SSL.
- **Reliability:** Multi-AZ, clustering.
- **Performance:** Petabyte-scale indexing and search capabilities.
- **Cost:** Pay per provisioned node.

---

This document provides an in-depth guide to AWS databases, their use cases, and considerations for Solutions Architects. 🚀