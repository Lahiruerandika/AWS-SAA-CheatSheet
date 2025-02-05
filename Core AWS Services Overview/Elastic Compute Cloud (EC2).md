# EC2

## Overview

EC2 mainly consists of the following capabilities:

- Renting virtual machines in the cloud (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across multiple machines (ELB)
- Scaling the services using an auto-scaling group (ASG)

## Introduction to Security Groups (SG)

- Security Groups are the fundamental aspect of networking security in AWS.
- They control how traffic is allowed into or out of EC2 instances.
- Essentially, they function as firewalls.

## Security Groups Deep Dive

- Security groups regulate:
  - Access to ports
  - Authorized IP ranges - IPv4 and IPv6
  - Control of inbound and outbound network traffic
- Security groups can be attached to multiple instances.
- They are locked down to a region/VPC combination.
- They function outside of EC2 instances—if traffic is blocked, the instance won't see it.
- **Best Practice**: Maintain a separate security group for SSH access.
- Troubleshooting:
  - If a request times out, it's likely a security group issue.
  - If a request returns "connection refused," it is likely an application issue (traffic reached the instance but the application is not responding).
- By default:
  - **All inbound traffic is blocked**
  - **All outbound traffic is allowed**
- Security groups can allow traffic from other security groups by referencing them directly instead of using instance IPs.

## Elastic IP

- When an EC2 instance is stopped and restarted, its public IP address may change.
- To maintain a fixed public IP, use **Elastic IP**.
- **Elastic IP** is a public IP owned by the user until it is released.
- It allows rapid failover by remapping the address to another instance.
- AWS provides a soft limit of **5 Elastic IPs** per account.
- **Best Practice**: Avoid using Elastic IPs when possible; instead, use DNS names mapped to dynamic public IPs.

## EC2 User Data

- EC2 instances can be **bootstrapped** using EC2 User Data scripts.
- User Data scripts run **only once** during the first instance launch.
- User Data scripts automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading files from the internet
  - Other startup configurations
- EC2 User Data scripts run with **root** privileges.

## EC2 Instance Launch Types

- On Demand Instances: short workload, predictable pricing
- Reserved: known amount of time (minimum 1 year). Types of reserved instances:
    - Reserved Instances: recommended long workloads
    - Convertible Reserved Instances: recommended for long workloads with flexible instance types
    - Scheduled Reserved Instances: instances reserved for a longer period used at a certain schedule 
- Spot Instances: for short workloads, they are cheap, but there is a risk of losing the instance while running
- Dedicated Instances: no other customer will share the underlying hardware
- Dedicated Hosts: book an entire physical server, can control the placement of the instance

### EC2 On Demand

- Pay for what we use, billing is done per second after the first minute
- Has the higher cost but it does not require upfront payment
- Recommended for short-term and uninterrupted workloads, when we can't predict how the application will behave

### EC2 Reserved Instances

- Up to 75% discount compared to On-demand
- Pay upfront for a given time, implies long term commitment
- Reserved period can be 1 or 3 years
- We can reserve a specific instance type
- Recommended for steady state usage applications (example: database)
- **Convertible Reserved Instances**:
    - The instance type can be changed
    - Up to 54% discount
- **Scheduled Reserved Instances**:
    - The instance can be launched within a time window
    - It is recommended when is required for an instance to run at certain times of the day/week/month

### EC2 Spot Instances

- We can get up to 90% discount compared to on-demand instances
- It is recommended for workloads which are resilient to failure since the instance can be stopped by the AWS if our max price is less than the current spot price
- Not recommended for critical jobs or databases
- Great combination: reserved instances for baseline performance + on-demand and spot instances for peak times

### EC2 Dedicated Hosts

- Physical dedicated EC2 server
- Provides full control of the EC2 instance placement
- It provides visibility to the underlying sockets/physical cores of the hardware
- It requires a 3 year period reservation
- Useful for software that have complicated licensing models or for companies that have strong regulatory compliance needs

### EC2 Dedicated Instances

- Instances running on hardware that is dedicated to a single account
- Instances may share hardware with other instances from the same account
- No control over instance placement
- Gives per instance billing

## EC2 Spot Instances - Deep Dive

- With a spot instance we can get a discount up to 90%
- We define a max spot price and get the instance if the current spot price < max spot price
- The hourly spot price varies based on offer and capacity
- If the current spot price goes over the selected max spot price we can choose to stop or terminate the instance within the next 2 minutes
- Spot Block: block a spot instance during a specified time frame (1 to 6 hours) without interruptions. In rare situations an instance may be reclaimed
- Spot request - with a spot request we define:
    - Maximum price
    - Desired number of instances
    - Launch specifications
    - Request type:
        - One time request: as soon as the spot request is fulfilled the instances will be launched and the request will go away
        - Persistence request: we want the desired number of instances to be valid as long as the spot request is active. In case the spot instances are reclaimed, the spot request will try to restart the instances as soon as the price goes down
- Cancel a spot instance: we can cancel spot instance requests if it is in open, active or disabled state (not failed, canceled, closed)
- Canceling a spot request does not terminate the launched instances. If we want to terminate a spot instance for good, first we have to cancel the spot request and then we can terminate the associated instances, otherwise the spot request may relaunch them

### Spot Fleet

- Spot Fleet is a set of spot instances and optional on-demand instances
- The spot fleet will try to meet the target capacity with price constraints
- AWS will launch instances from a launch pool, meaning we have to define the instance type, OS, AZ for a launch pool
- We can have multiple launch pools from within the best one is chosen
- If a spot fleet reaches capacity or max cost, no more new instances are launched
- Strategies to allocate spot instances in a spot fleet:
    - **lowerPrice**: the instances will be launched from the pool with the lowest price
    - **diversified**: launched instances will be distributed from all the defined pools
    - **capacityOptimized**: launch with the optimal capacity based on the number of instances

## AMI

- AWS comes with lots of base images
- Images can be customized ar runtime with EC2 User data
- In case of more granular customization AWS allows creating own images - this is called an AMI
- Advantages of a custom AMI:
    - Pre-install packages
    - Faster boot time (on need for the instance to execute the scripts from the user data)
    - Machine configured with monitoring/enterprise software
    - Security concerns - control over the machines in the network
    - Control over maintenance
    - Active Directory out of the box
- An AMI is built for a specific region (NOT GLOBAL!)

### Public AMI

- We can leverage AMIs from other people
- We can also pay for other people's AMI by the hour, basically renting the AMI form the AWS Marketplace
- Warning: do not use AMI which is not trustworthy!

### AMI Storage

- An AMI takes space and they are stored in S3
- AMIs by default are private and locker for account/region
- We can make our AMIs public and share them with other people or sell them on the Marketplace

### Cross Account AMI Sharing

- It is possible the share AMI with another AWS account
- Sharing an AMI does not affect the ownership of the AMI
- If a shared AMI is copied, than the account who did the copy becomes the owner
- To copy an AMI that was shared from another account, the owner of the source AMI must grant read permissions for the storage that backs the AMI, either the associated EBS snapshot or an associated S3 bucket
- Limits:
    - An encrypted AMI can not be copied. Instead, if the underlying snapshot and encryption key where shared, we can copy the snapshot while re-encrypting it with a key of our own. The copied snapshot can be registered as a new AMI
    - We cant copy an AMI with an associated **billingProduct** code that was shared with us from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with **billingProduct** code, we have to launch an EC2 instance from our account using the shared AMI and then create an AMI from source

## Placement Groups

- Sometimes we want to control how the EC2 instances are placed in the AWS infrastructure
- When we create a placement group, we can specify one of the following placement strategies:
    - **Cluster** - cluster instances into a low-latency group in a single AZ
    - **Spread** - spread instances across underlying hardware (max 7 instances per group per AZ)
    - **Partition** - spread instances across many different partitions (which rely on different sets of racks) within an AZ. Scale to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)

### Placement Groups - Cluster

- Pros: Great network (10Gbps bandwidth between instances)
- Cons: if the rack fails, all instances fail at the time
- Use cases:
    - Big data job that needs to complete fast
    - Application that needs extremely low latency and high network throughput

### Placement Groups - Spread

- Pros:
    - Can span across multiple AZs
    - Reduces risk for simultaneous failure
    - EC2 instances are on different hardware
- Cons:
    - Limited to 7 instances per AZ per placement group
- Use case:
    - Application that needs to maximize high availability
    - Critical applications where each instance must be isolated from failure

### Placement Groups - Partitions

- Pros:
    - Up to 7 partitions per AZ
    - Can have hundreds of EC2 instances per AZ
    - The instances in a partition do not share racks with the instances from other partitions
    - A partition failure can effect many instances but they wont affect other partitions
    - Instances get access to the partition information as metadata
- Use cases: HDFS, HBase, Cassandra, Kafka

## Elastic Network Interfaces - ENI

- Logical component in a VPC that represents a virtual network card
- An ENI can have the following attributes:
    - Primary private IPv4 address, one or more secondary IPv4 addresses
    - One Elastic IP (IPv4) per private IPv4
    - One Public IPv4
- ENI instances can be created independently from an EC2 instance
- We can attach them on the fly to an EC2 instances or move them from one to another (useful for failover)
- ENIs are bound to a specific available zone
- ENIs can have security group attached to them
- EC2 instances usually have a primary ENI (eth0). In case we attach a secondary ENI, eth1 interface will be available. The primary ENI can not be detached.

## EC2 Hibernate

- We can stop or terminate EC2 instances:
    - If an instance is stopped: the data on the disk (EBS) is kept intact
    - If an instance is terminated: any root EBS volume will also gets destroyed
- On start, the following happens in case of an EC2 instance:
    - Fist start: the OS boots and EC2 User data script is executed
    - Following starts: the OS boots
    - After the OS boot the applications start, cache gets warmed up, etc. which may take some time
- EC2 Hibernate:
    - All the data from RAM is preserved on shut-down
    - The instance boot is faster
    - Under the hood: the RAM state is written to a file in the root EBS volume
    - The root EBS volume must be encrypted
- Supported instance types for hibernate: C3, C4, C5, M3, M4, M5, R3, R4, R5
- Supported OS types: Amazon Linux 1 and 2, Windows
- Instance RAM size: must be less then 150 GB
- Bare metal instances do not support hibernate
- Root volume: must be EBS, encrypted, not instance store. And it must be large enough
- Hibernate is available for on-demand and reserved instances
- An instance can not hibernate for more than 60 days

## EBS Volume Types - Deep Dive

### GP2

- Recommended for most workloads
- Can be system boot volume
- Can be used for virtual desktops, low-latency applications, development and test environments
- Size can range from 1GiB to 16TiB
- Small GP2 volumes can burst IOPS to 3000
- Max IOPS is 16000
- We get 3 IOPS per GiB, which means at 5334GiB we are the max IOPS size

### IO1 

- Recommended for business critical applications which require sustained IOPS performance, or more than 16000 IOPS per volume
- Recommended for large database workloads
- Size can be between 4Gib and 16 TiB
- The maximum ratio of provisioned IOPS per requested volume size is 50:1
- Max IOPS for IO1/2 volumes is 64000 IOPS for instances built on Nitro System and 32000 for other type of instances

### ST1

- Recommended for streaming workloads
- It has fast throughput at low price
- Can not be a root volume
- Size can be between 500Gib and 16TiB
- Max IOPS is 500
- Max throughput 500 MiB/Sec

### SC1

- Throughput oriented storage for large volumes of data which is infrequently accessed
- Can not be a boot volume
- Max IOPS is 250, max throughput 250MiB/sec

### Limits

- SSD, General Purpose – gp2
    – Volume size 1 GiB – 16 TiB
    – Max IOPS/volume 16,000
- SSD, Provisioned IOPS – i01
    – Volume size 4 GiB – 16 TiB
    – Max IOPS/volume 64,000
– HDD, Throughput Optimized – (st1)
    – Volume size 500 GiB – 16 TiB 
    - Throughput measured in MB/s, and includes the ability to burst up to 250 MB/s per TB, with a baseline throughput of 40 MB/s per TB and a maximum throughput of 500 MB/s per volume
- HDD, Cold – (sc1)
    – Volume size 500 GiB – 16 TiB.
    - Lowest cost storage – cannot be a boot volume
– These volumes can burst up to 80 MB/s per TB, with a baseline throughput of 12 MB/s per TB and a maximum throughput of 250 MB/s per volume: HDD, Magnetic – Standard – cheap, infrequently accessed storage – lowest cost storage that can be a boot volume

## EBS Snapshots

- Snapshots are incremental - only the changed blocks are backed up
- EBS backups use IO and we should not run them while the application is handling a lot of traffic
- Snapshots are stored in S3 (we are not able to see them)
- It is not necessary to detach the volume to do a snapshot, but it is recommended
- An account can have up to 100k snapshots
- We can make an image (AMI) out of a snapshot, snapshots can be copied across AZs
- EBS volumes restored from snapshots need to be pre-warmed (using `fio` or `dd` commands to read the entire volume)
- Snapshots can be automated using **Amazon Data Lifecycle Manager**

## EBS Migrations

- EBS Volumes are locked to a specific AZ
- To migrate it to a different AZ (or region) we have to do the following:
    - Create a snapshot from the volume
    - (optional) Copy the volume to a different region
    - Create a volume from the snapshot in the AZ of choice

## EBS Encryption

- When we create an encrypted EBS volume, we get the following:
    - Data at rest is encrypted inside the volume
    - All the data in flight moving between the instance and the volume is encrypted
    - All snapshots are encrypted
    - All volumes created from the snapshots will be encrypted
- Encryption and decryption are handled transparently by EBS system
- Encryption may have a minimal impact on latency
- EBS Encryption leverages keys from KMS (encryption algorithm is AES-256)
- Copying an unencrypted snapshot allows encryption
- Encrypt an unencrypted EBS volume:
    1. Create an EBS snapshot from the volume
    2. Copy the snapshot an enable encryption on the process
    3. Create a new EBS volume from the snapshot (the volume will be encrypted)
    4. Attach the encrypted volume to an instance

## EBS vs Instance Store

- Some instances do not come with a root EBS volume
- Instead, they come with an **instance store** (ephemeral storage)
- An instance store is  a physically attached to the machine (EBS is a network drive)
- Pros of instance stores:
    - Better I/O performance
    - Good for buffer, cache, scratch data, temporary content
    - Data survives a reboot
- Cons of instance stores:
    - On stop or termination of the instance, the data from the instance store is lost
    - An instance store can not be resized
    - Backups of an instance store must be done manually by the user
- An instance store is:
    - A physical disk form the physical server where the EC2 instance runs
    - Very Hight IOPS disk
    - A disk up to 7.5 TiB, stripped to reach 30 TiB
    - A block storage (just like EBS)
    - Can not be increased in size
    - An ephemeral storage (risk of data loss if hardware fails)

## EBS RAID Options

- EBS is already redundant storage (replicated within an AZ)
- If we want to increase IOPS of if we want to mirror an EBS volume we can mount EBS volumes in parallel RAID settings
- RAID is possible as long as the OS supports it
- Some RAID options are:
    - RAID 0
    - RAID 1
    - RAID 5, RAID 6 are not recommended for EBS
- **RAID 0**: used for increased performance. We can combine to or more volumes and what we get is the total number of disk space and I/O
    - If one of the disks fail, all the logical data is lost
    - Use cases:
        - Applications with lot of IOPS but without the need for fault-tolerance
        - A database with builtin replication
- **RAID 1**: used for increased fault-tolerance. Mirroring a volume to another.
    - If one the disks fails, the logical volume will still work
    - We have to send the data to two EBS volumes at the same time
    - Use cases:
        - Applications that need increased fault-tolerance
        - Applications which need to service disks