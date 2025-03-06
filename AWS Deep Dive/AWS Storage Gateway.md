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
