# Amazon S3

**Amazon S3** (Simple Storage Service) is one of the main building blocks of AWS, offering "infinitely scaling" storage. It’s designed for storing and retrieving any amount of data at any time, from anywhere.

## S3 Buckets

- Amazon S3 stores objects (files) in **buckets**.
- **Buckets must have a globally unique name** across all AWS accounts.
- Buckets are created within specific **regions**.
  
### Bucket Naming Conventions:
- **No uppercase letters**.
- **No underscores**.
- Name must be **3-63 characters** long.
- **Cannot be an IP address** (e.g., 192.168.1.1).
- Must start with a **lowercase letter** or **number**.

## S3 Objects

- An **object** in a bucket is a file stored in S3.
- Each object is identified by a **key** (essentially its full path), e.g.:
    - `s3://my-bucket/my_file.txt`
    - `s3://my-bucket/my_folder/another_folder/my_file.txt`
- The **key** consists of a **prefix** + **object name**:
    - `s3://my-bucket/my_folder/another_folder/my_file.txt`
- S3 does not use traditional **directories** in the way file systems do; instead, it uses keys with slashes ("/") to mimic directories.
  
### Object Details:
- **Max object size** in S3 is **5 TB**.
- For uploads **larger than 5 GB**, **multi-part upload** is required.
- Objects can have **metadata** (key-value pairs), which can be either system or user-defined.
- Objects can also have **tags** (Unicode key-value pairs) for purposes such as security and lifecycle management. A bucket can have up to **10 tags** per object.
- If versioning is enabled, each object will have a **version ID**.

## S3 Versioning

Versioning in S3 allows you to keep multiple versions of an object in the same bucket.

### Key Points:
- **Versioning** must be enabled at the **bucket level**.
- When a file with the **same key** (name) is uploaded, S3 will create a new version of the object. The previous version won't be overwritten; both versions will coexist.
  
### Benefits of Versioning:
- Protects files against unintended deletion.
- Enables rollback to previous versions if needed.
  
### Additional Notes:
- Files uploaded **before versioning is enabled** will have the version "null".
- **Suspending versioning** does not delete previous versions.
  
### Deleting Versioned Files:
- When a versioned file is deleted, a **delete marker** is added. The file is not deleted but can be restored by removing the delete marker.
- To **permanently delete** the file, both the delete marker and the object must be deleted.

## S3 Security

### Encryption at Rest

- AWS provides 4 methods of encryption for objects in S3
    1. SSE-S3: encrypts S3 objects using keys handled and managed by AWS
    2. SSE-KMS: leverage AWS Key Management Service to manage encryption keys
    3. SSE-C: the encryption keys are managed by the user
    4. Client Side Encryption
- SSE-S3:
    - Keys used for encryption is managed by Amazon S3
    - Objects are encrypted in the server side
    - It uses AES-256 encryption
    - In order to have SSE-S3 encryption clients must set a header, which is **x-amz-server-side-encryption": "AES256"**
- SSE-KMS:
    - Encryption keys are handled and managed by KMS
    - KMS allows the manage which keys will be used for the encryption, moreover it has audit trails in order to be able to see who was using the KMS key
    - Objects are encrypted in the server-side
    - In order to have SSE-S3 encryption clients must set a header, which is **x-amz-server-side-encryption": "aws:kms"**
- SSE-C:
    - Server side encryption using data keys provided by the user from the outside of AWS
    - Amazon S3 does not store the encryption key provided by the user
    - Data should be transmitted through HTTPS, because a key is sent the AWS
    - Encryption key must be provided in the header of the request for every request
    - When retrieving the object, the same encryption key must be provided in the header
- Client Side Encryption:
    - Data must be encrypted before sending it to S3
    - This is usually accomplished by using a third party encryption library, like Amazon S3 Encryption Client
    - The user is solely responsible for encryption-decryption
    - The keys and the encryption cycle is managed by the user

### Encryption in transit (SSL/TLS)

- Amazon S3 exposes:
    - HTTP endpoint for non-encrypted data
    - HTTPS endpoint for encryption in flight which relies on SSL/TLS
- Most clients for S3 will use HTTPS by default
- In case of SSE-C encryption HTTPS in mandatory

### S3 Security Overview

- User based security:
    - Accomplished by using IAM policies: specified which calls should be allowed for a specified sued from IAM console
- Resource based security:
    - Accomplished by using bucket policies which are bucket wide rules from the S3 console. These rules may allow cross account access to the bucket
    - We also have Object Access Control Lists (ACL) and Bucket Access Control Lists which allow finer grain control over the bucket
Note: an IAM principle can access an S3 object if:
    - The user IAM permission allows it or the resource policy allows it
    - The is no explicit deny

### S3 Bucket Policies

- Bucket policies are JSON based documents
- They can be applied to both buckets and objects in buckets
- The effect of a statement in the bucket policy can be either allow or deny
- The principle in the policy represents the account or the user for which the policy applies to
- Common use cases for S3 bucket policies:
    - Grant public access to the bucket
    - Force objects to be encrypted at the upload
    - Grant access to another account (cross account access)

### Bucket Settings for Block Public Access

- Relatively new settings that was created to block public access to buckets and objects if the account has some restrictions:
- S3 provides 4 different kind of block public access settings:
    - new access control lists
    - any access control lists
    - new public bucket or access point policies
    - block public and cross-account access to buckets and objects through any public bucket or access point policies
- These settings were created to prevent company data leaks

### S3 Other Security Features

- Networking:
    - S3 supports VPC Endpoints (for instances in VPC without internet access)
- Logging and Audit:
    - S3 Access Logs can be stored in other S3 buckets
    - API calls can be logged in AWS CloudTrail
- User Security:
    - MFA Delete can be required in versioned buckets in order to protect for accidental deletions
    - Pre-Signed URLs: ULRs that are valid only for a limited time

## S3 Websites

- S3 can host static websites and have them accessible from the internet
- The website URL will be something like this:
    - `<bucket-name>.s3-website-<AWS-region>.amazonaws.com`
    - `<bucket-name>.s3-website.<AWS-region>.amazonaws.com`
- In case of `403` errors we have to make sure that the bucket policy allows public reads

### CORS

- An origin is a scheme (protocol), host (domain) or port
- CORS: Cross Origin Resource Sharing
- CORS is a web browser based mechanism to allow requests to other origins while visiting the main one
- Same origin example: http://example.com/app1 and http://example.com/app2
- Different origins: http://example.com and http://otherexample.com
- The request wont be fulfilled unless the other origin allows for the request, using CORS headers (example: Access-Control-Allow-Origin, Access-Control-Allow-Method)

### S3 CORS

- If a client does a cross-origin request on an S3 bucket, the correct CORS headers need to be enabled in order for the request to succeed
- Request can be allowed for a specified origin (by specifying the URL of the origin) or for all origins (by using *)

