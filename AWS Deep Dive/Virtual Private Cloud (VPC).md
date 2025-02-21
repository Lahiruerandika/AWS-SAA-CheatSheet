# Networking - VPC

## CIDR - Classless Inter-Domain Routing

- CIDR is used for Security Group rules and AWS networking in general
- It is used to define an IP address range
    - ww.xx.yy.zz/32 - one IP address
    - 0.0.0.0/0 - all possible IP addresses
    - 192.168.0.0/26 - range of 192.168.0.0 - 192.168.0.63 64 IP addresses
- CIDR has to component:
    - The base IP: represents an IP from a given the range
    - The subnet mask: defines how many bits can change in the IP
- The subnet mask can take 2 forms:
    - 255.255.255.0 - less common
    - /24 - more common
- The subnet mask basically allows a part of the base IP to get additional next values:
    - /32 allows for 1 IP => 2^0
    - /31 allows for 2 IPS => 2^1
    - /30 allows for 4 IPs => 2^2
    - /29 allows for 8 IPs => 2^3
    ...
    - /0 allows for 2^31 IPs, all IPs
- Most used subnet masks:
    - /32 - no IP number can change
    - /24 - last IP number can change (256 IP addresses)
    - /16 - last 2 IP numbers can change (65536 IP addresses)
    - /8 - last three IP numbers can change
    - /0 - all the IP numbers can change
- To calculate CIDR, use: https://www.ipaddressguide.com/cidr

## Private vs Public IP Addresses (IPv4)

- Private IP can only allow certain values:
    - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) - used for big networks
    - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) - default AWS private VPC
    - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) - home networks
- All the rest of the IP addresses are considered public

## Default VPC

- All new accounts have a default VPC
- New instances are launched into default VPC if no subnet is specified
- Default VPCs have internet connectivity and all instances have public IP address
- We also get a public and a private DNS name

## VPC - Virtual Private Cloud

- We can have multiple VPCs in a region (max 5 per region - soft limit)
- Max CIDR per VPC is 5, for each CIDR:
    - Min size is /28 = 16 IP addresses
    - Max size is /16 = 65K IP addresses
- VPC is private => only the private address ranges are allowed
- **A newly created VPC CIDR should not overlap with an existing one used another VPC**

## VPC Subnets

- Subnets are tied to specific AZs
- AWS reservers 5 IP addresses (first 4 and the last 1 address) in each subnet
- These 5 IP addresses are not available and can not be assigned to an instance
- Example, in case of a CIDR block 10.0.0.0/24 the reserver IPs are the following:
    - 10.0.0.0 - Network address
    - 10.0.0.1 - Reserved by AWS for the VPC router
    - 10.0.0.2 - Reserved by AWS for mapping to an Amazon provided DNS
    - 10.0.0.3 - Reserved for future use
    - 10.0.0.255 - Network broadcast address. AWS does not supports broadcast in a VPC, therefore the address is reserved

## IGW - Internet Gateways

- Internet gateways helps a VPC instance to connect to the internet
- It scales horizontally and is HA and redundant
- Must be created separately from a VPC
- One VPC can have only one attached internet gateway, one internet gateway can have only one VPC
- Internet Gateway is also a NAT for the instances that have a public IPv4
- Internet Gateways on their one do not allow internet access, route tables also must be configured

## NAT Instances - Network Address Translation (outdated)

- Allow instances in private subnets to connect to the internet
- NAT instances must be launched in a public subnet to have internet access
- *Source/Destination Check* flag for EC2 must be disabled
- NAT instanced should have an Elastic IP attached to them
- Route tables must be configured to route traffic from the private subnet to the NAT instance
- In order to set up we must use a pre-configured Amazon Linux AMI
- It is not HA/resilient out of the box => We would need to set up an ASG in multi AZ + resilient user data script
- Internet traffic bandwidth depends on the EC2 instance performance

## NAT Gateway

- AWS managed NAT, higher bandwidth, better availability, no administration
- It is pay by hour for usage and bandwidth
- NAT is created in a specific AZ and it uses an Elastic IP
- It can not be used by an instance from the same subnet as the NAT
- Required an IGW
- 5Gbps of bandwidth with automatic scaling up to 45Gbps
- There is no security group to manage
- NAT Gateway is resilient within a single AZ
- We must create multiple NAT Gateways in multiple AZs for fault-tolerance

## Comparison between NAT Instance and NAT Gateway

- AWS comparison: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html

## DNS Resolution in VPC

-DNS Resolutions settings:
    - **enableDnsSupport**:
        - By default is set to true
        - Helps decide if DNS resolution is supported for the VPC
        - If true, queries the AWS DNS server at 169.254.169.253
    - **enableDNSHostName**:
        - By default is set to false for an user created VPC, true for the Default VPC
        - Won't do anything unless enableDnsSupport=true
        - If true, the VPC assigns public host names to EC2 instances
- If we use custom DNS domain names in a private zone in Route53, we must set both of these attributes to true

## Network Access Control Lists (NACL) and Security Groups (SG)

- NACL is a like a firewall which controls traffic which goes outside of comes inside a subnet
- The default NACL allows everything outbound and everything inbound
- We define one NACL per subnet, new subnets are assigned the default NACL
- We can define NACL rules:
    - Rules have a number (1 - 32766) which defines the precedence
    - Rules with lower number have higher precedence
    - Rule with higher precedence wins at the time of evaluation
    - Last rule is has the precedence of asterisk (*) and denies all the requests. This rule is not editable
    - AWS recommends adding rules by increment of 100
- Newly created created NACL will deny everything (last rule)
- NACLs are great way of blocking a specific IP address at the subnet level

| Security Group                                           |  Network ACL                                                            |
|----------------------------------------------------------|-------------------------------------------------------------------------|
| Operates at the instance level                           | Operates at the subnet level                                            |
| Supports allow rules only                                | Supports allow rules and deny rules                                     |
| It is stateful: return traffic is automatically allowed  | It is stateless: return traffic must be explicitly allowed by the rules |
| All rules are evaluated before deciding to allow traffic | Rules have a precedence when deciding whether to allow or deny traffic  |
| It is associated to an instance inside of a VPC          | Automatically applies to all instances in the subnet                    |

- Example of NACL with ephemeral ports: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html