# Storage Gateway

## Hybrid Cloud for Storage

- Hybrid cloud:
    - Part of a company's infrastructure is in the public cloud (like AWS)
    - Part of a company's infrastructure is on-premise
- S3 is a proprietary storage technology (unlike EFS/NFS), it can be exposed to on-premise servers through a storage gateway

## Storage Gateway Introduction

- Bridge between on-premise data and cloud data in S3
- Uses cases for storage gateway with S3: disaster recovery, backup and restore, tiered storage
- AWS provides 3 types of storage gateways:
    - **File Gateway**: allows us to view files from the local files system, but this files are backed by S3
    - **Volume Gateway**: same as file gateway but with volumes
    - **Tape Gateway**: used for backup and recovery

### File Gateway

- Configured S3 buckets are accessible using NFS and SMB protocols
- Supports S3 Standard, S3 IA, One Zone IA
- Each buckets will have its own IAM roles in order to be accessed by the file gateway
- Most recently used data is cached in the file gateway
- File Gateway can be mounted on many servers (because of the NFS protocol)
