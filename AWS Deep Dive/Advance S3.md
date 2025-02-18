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
