# DynamoDB

- Fully managed, highly available with replication across 3 AZs
- NoSQL database - not a relational database
- Scales to massive workloads, distributed database
- Millions of requests per seconds, trillions or rows, hundreds of thousands of TB of storage
- It is fast and consistent regarding performance (low latency retrieval of data)
- It is integrated with IAM for security, authorization and administration
- It enables event driven programming with DynamoDB Streams
- It provides auto scaling capabilities at low cost

## Basics

- DynamoDB is made of tables
- Each table has a primary key (must be decided at creation time)
- Each table can have an infinite number of items (rows)
- Each item has attributes which can be added over time (can be null)
- Maximum size of an item is 400KB
- Supported data types:
    - Scalar types: string, number binary, null
    - Document types: list, map
    - Set types: string set, number set, binary set

## Provisioned Throughput

- Table must have a provisioned throughput, we must provision read and write capacity units
- Read Capacity Unit (RCU): throughput for reads ($0.00013 per RCU)
    - 1 RCU = 1 strongly consistent read of 4 KB per second
    - 1 RCU = 2 eventually consistent read of 4 KB per second
- Write Capacity Unit (WCU): throughput for writes ($0.00065 per WCU)
    - 1 WCU =  1 write of 1 KB per second
- Option to setup auto-scaling of throughput to meet demand
- Throughput can be exceeded temporarily using burst credits
- If there are no more burst credits, we may get a "ProvisionedThroughputException" in which case it is advised to do exponential back-off retry
