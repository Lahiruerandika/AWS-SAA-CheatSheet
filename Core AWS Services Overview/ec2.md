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
