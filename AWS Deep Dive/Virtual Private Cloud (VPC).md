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
