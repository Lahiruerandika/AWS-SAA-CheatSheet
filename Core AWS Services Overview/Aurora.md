# Amazon Aurora

- Aurora is a proprietary technology from AWS (not open sourced)
- It provides support for both PostgreSQL and MySQL drivers in order to be able to connect to it
- Aurora is cloud optimized, it claims 5x performance over MySQL and over 3x performance over PostgreSQL
- Aurora storage automatically grows in increments from 10GB up to 64TB
- Aurora can have 15 replicas (while MySQL has only 5), replication process is faster
- Failover is Aurora is instantaneous
- Aurora costs more than classic RDS (around 20%)
- Aurora availability:
    - Stores 6 copies of the data across 3 AZs - only needs 4 copies for writes and 3 for reads
    - It has self healing properties with peer-to-peer replication
    - Storage is split across 100s of volumes
- In Aurora only one instance is used for writes (master instance)
- In case of master failure, the failover happens in less than 30 seconds
- Provides support for cross region replication