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
