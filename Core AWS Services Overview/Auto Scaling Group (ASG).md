# Auto Scaling Groups

- Applications may encounter different amount of load depending on their usage span
- In cloud we can create and get rid of resources (servers) quickly
- The goal of an Auto Scaling Group (ASG) is to:
    - Scale out (add more EC2 instances) to match the increased load
    - Scale in (remote EC2 instances) to match a decreased load
    - Ensure we have a minimum and a maximum number of machines running
    - Automatically register new instances to a load balancer

## ASG Attributes

- Launch configuration - consists of:
    - AMI + Instance Type
    - EC2 User Data
    - EBS Volumes
    - Security Groups
    - SSH Key Pair
- Min size, max size, initial capacity
- Network + subnets information
- Load balancer information
- Scaling policies - what will trigger a scale out/scale in

## Auto Scaling Alarms

- It is possible to scale an ASG based on CloudWatch alarms
- An alarm monitors a metric (such as Average CPU)
- **Metrics are computed for the overall ASG instances**
- Based on alarms we can create:
    - Scale-out policies
    - Scale-in policies

## Auto Scaling New Rules

- It is possible to define "better" auto scaling rules managed directly by EC2 instances, for example:
    - Target Average CPU Usage
    - Number of requests on teh ELB per instance
    - Average Network In/Out
- These rules are easier to set up and to reason about then the previous ones

## Auto Scaling Based on Custom Metrics

- We can scale based on a custom metric (ex: number of connected users to the application)
- In order to do this we have to:
    1. Send a custom metric request to CloudWatch (PutMetric API)
    2. Create a CloudWatch alarm to react to values of the metric
    3. Use the CloudWatch alarm as a scaling policy for ASG