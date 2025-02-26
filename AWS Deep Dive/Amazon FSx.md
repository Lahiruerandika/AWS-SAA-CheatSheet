# Amazon FSx Overview

- Launch 3rd party high-performance file systems on AWS
- Fully managed service
  - 1. Amazon FSx for Windows (File Server)
  - 2. Amazon FSx for Lustre
  - 3. Amazon FSx for NetApp ONTAP
  - 4. Amazon FSx for OpenZFS

## Amazon FSx for Windows
- FSx for Windows is a fully managed Windows file system share drive 
  - Suppor ts SMB protocol & Windows NTFS
  - MicrosoftActiveDirectoryintegration,ACLs,userquotas
  - Can be mounted on Linux EC2 instances
  - Supports Microsoft's Distributed File System (DFS) Namespaces (group files across multiple FS) - Scale up to 10s of GB/s, millions of IOPS, 100s PB of data
  - Storage Options:
    - SSD – latency sensitive workloads (databases, media processing, data analytics, ...) 
    - HDD – broad spectrum of workloads (home directory, CMS, ...)
  - Can be accessed from your on-premises infrastructure (VPN or Direct Connect) 
  - Can be configured to be Multi-AZ (high availability)
  - Data is backed-up daily to S3