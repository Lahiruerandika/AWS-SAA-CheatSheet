# EBS - Elastic Block Storage

- An EC2 instances loses its root volume when it is manually terminated
- Unexpected terminations may happen
- Sometimes we need a way to store instance data somewhere
- An EBS (Elastic Block Store) Volume is a network drive which can be attached to an EC2 instance
- It allows for the instances to persist date
- EBS is a network drive:
    - It uses the network to communicate with the instance, which can introduce latency
    - It can be detached from an EC2 and attached ot another
- EBS volumes are locked to an AZ
- To move a volume across, we need to create a snapshot
- EBS volumes have a provisioned capacity (size in GB and IOPS)
- Billing is done for all provisioned capacity even if the capacity is not fully used

## EBS Volume Types

- EBS Volumes can have 4 types:
    - GP2 (SSD): general purpose SSD volume that balances price and performance
    - IO1 (SSD): highest performance SSD volume for mission-critical low-latency or high-throughput workloads
    - ST1 (HDD): low cost HDD volume designed for frequent access, throughput-intensive workloads
    - SC1 (HDD): for less frequently accessed data
- EBS Volumes are characterized in Size | Throughput | IOPS (I/O Operations per second)
- Only GP2 and IO1 can be used as boot volumes
