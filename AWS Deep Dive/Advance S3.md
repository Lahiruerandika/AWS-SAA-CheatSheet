# Advanced S3

## S3 MFA-Delete

- To use MFA-Delete, we must enable versioning on the selected bucket.
- MFA will be required when:
    - Permanently deleting an object version.
    - Suspending versioning on the bucket.
- MFA won't be required when:
    - Enabling versioning.
    - Listing deleted versions.
    - Adding a delete marker to an object.
- **MFA-Delete can be enabled/disabled only by the bucket owner (root account)!**
- MFA-Delete can only be enabled using the CLI.

## S3 Access Logs

- For audit purposes, we may want to log all access to S3 buckets.
- Any request made to S3, from any account (authorized or denied), will be logged into another S3 bucket.
- The data can be analyzed using data analysis tools or Amazon Athena.

### Warnings

- We should never set our logging bucket as the monitored bucket! This may create a logging loop, causing the bucket size to grow exponentially.

## S3 Replication

- To enable replication:
    - Versioning must be enabled on both the source and destination buckets.
- There are two types of replication:
    - **Cross-Region Replication (CRR):** Buckets are in different regions.
        - Used for compliance, lower latency access, and replication across accounts.
    - **Same-Region Replication (SRR):** Buckets are in the same region.
        - Used for log aggregation and live replication between production and test accounts.
- In both cases, the buckets can be in separate accounts.
- Copying between replica buckets happens asynchronously (it is very quick).
- To copy between replicas, an IAM permission must be assigned to the source bucket.

### Replication Notes

- Only new objects are replicated after replication is activated (no retroactive replication).
- For **DELETE** operations:
    - Deletion **without** a version ID: A delete marker is added to the object. **Deletion is not replicated**.
    - Deletion **with** a version ID: The object is deleted in the source bucket. **Deletion is not replicated**.
- **There is no replication chaining!**

## S3 Pre-Signed URLs

- We can generate pre-signed URLs using the SDK and the CLI.
- Pre-signed URLs have a default expiration time of **3600 seconds**. This can be changed using the `--expires-in` argument.
- Users with a pre-signed URL will inherit the permissions of the user who generated the URL.

## S3 Storage Classes

- **Amazon S3 Standard - General Purpose**
- **Amazon S3 Standard - Infrequent Access (IA)**
- **Amazon S3 One Zone - Infrequent Access**
- **Amazon S3 Intelligent Tiering**
- **Amazon S3 Glacier**
- **Amazon S3 Glacier Deep Archive**
- **Amazon S3 Reduced Redundancy Storage (deprecated)**

### S3 Standard - General Purpose

- High durability (99.999999999% or **"11 nines"**) across multiple AZs.
- SLA: If we store 10 million objects in S3, we can expect to lose **one file per 10,000 years**.
- **99.99% availability** per year.
- Can sustain **two concurrent facility failures**.

### S3 Standard - Infrequent Access

- Suitable for data that is accessed less frequently but should be retrieved quickly when needed.
- **Same durability** as General Purpose, but **99.9% availability**.
- **Lower cost** than General Purpose.

### S3 One Zone - Infrequent Access

- Same as Standard IA, but data is stored in **a single AZ**.
- **Same durability** as Standard IA, but **data can be lost if the AZ goes down**.
- **99.5% availability** per year.
- **Lower cost** than IA.

### S3 Intelligent Tiering

- Automatically moves objects between two access tiers based on access patterns.
- Has a **small monthly monitoring fee**.
- **Same durability** as General Purpose, with **99.9% availability**.

### S3 Glacier

- **Low-cost object storage** for archiving/backup data.
- Data is retained for long-term storage (**decades**).
- Alternative to **on-premise magnetic tape** storage.
- **Same durability** as General Purpose.
- **Low monthly storage cost**, but **data retrieval incurs a fee**.
- Each item in Glacier is called an **archive**, and archives are stored in **vaults**.
- Provides **three retrieval options**:
    - **Expedited** (1 to 5 minutes) - **costs $10**.
    - **Standard** (3 to 5 hours).
    - **Bulk** (5 to 12 hours).
- **Minimum storage duration: 90 days**.

### S3 Glacier Deep Archive

- For **very long-term storage** - **cheaper than S3 Glacier**.
- **Retrieval options**:
    - **Standard** (12 hours).
    - **Bulk** (48 hours).
- **Minimum storage duration: 180 days**.
