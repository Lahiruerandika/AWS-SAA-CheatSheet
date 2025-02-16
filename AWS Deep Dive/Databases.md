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