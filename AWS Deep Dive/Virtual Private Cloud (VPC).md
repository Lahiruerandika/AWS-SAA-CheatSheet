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
