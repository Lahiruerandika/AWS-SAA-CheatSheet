# AWS Route 53 Configuration

## Overview
This guide provides step-by-step instructions to configure AWS Route 53 for a GitLab repository. Route 53 is a scalable and highly available Domain Name System (DNS) web service that helps route end-user requests to applications hosted on AWS.

## Route 53

- Route 53 is a Managed DNS (Domain Name System).
- DNS is a collection of rules and records that help clients understand how to reach a server through its domain name.
- In AWS, the most common records are:
  - **A**: Maps a hostname to an IPv4 address.
  - **AAAA**: Maps a hostname to an IPv6 address.
  - **CNAME**: Maps a hostname to another hostname.
  - **Alias**: Maps a hostname to an AWS resource.
- Route 53 can use:
  - Public domain names we own.
  - Private domain names that can be resolved by EC2 instances inside our VPCs.
- Route 53 has advanced features such as:
  - Load balancing through DNS (client load balancing).
  - Health checks.
  - Routing policies: simple, failover, geolocation, latency, weighted, multi-value.
- We pay $0.5 per month per hosted zone.