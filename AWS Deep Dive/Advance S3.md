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