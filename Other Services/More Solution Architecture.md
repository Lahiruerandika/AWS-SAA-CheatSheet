# More Solution Architecture

## Event Processing

- SQS + Lambda:
    - Lambda functions pulls the SQS queue, in case there is a problem, the message is put back onto the queue for reprocessing
    - To avoid endless loops in processing, we can set up a deal-letter queue (DLQ)
- SQS FIFO + Lambda:
    - If a message is not processed, it can block the whole queue
    - In order to get around this, we can also set up a DLQ
- SNS + Lambda:
    - In case a message is not processed, the Lambda will retry 3 times
    - We can also set up a DLQ at the Lambda service level
- Fan Out Pattern:
    - Deliver messages to multiple SQS queues
    - In order to achieve this, we can create an SNS topic and create SQS queue subscribers
    - We can combine Fan Out pattern with S3 events
    - We can also create filter to filter out some events and react to only what is needed
    - We can create as many S3 events as we want 
    - If two events are happening on the same object on the same time, there is a possibility that only one event notification is sent. To overcome this we can use versioning

## Caching Strategies

- CloudFront: caching happens globally as close as possible to the users
- API Gateway: offers regional caching
- Redis, Memcached, DAX: caching is closer to the application. The reason for this is to avoid load on a database

## Blocking an IP Address in AWS

- Network ACL, VPC level: create a deny rule
- Security Groups: define a subset of IP which can access the application
- Optional firewall installed on the instance
- In case of an Application Load Balancer:
    - ALB does connection termination, from the EC2 side we just have to approve traffic from the ALB
    - In the SG of the LB we can specify from where the traffic can came from
    - We can also install WAF on the ALB, where we can do some complex filtering
- In case of Network Load Balancer:
    - NLB does not do connection termination, there is no such thing as a SG for the NLB
- In case of CloudFront:
    - CloudFront seats outside of a VPC, so we can not set NACL rules
    - In this case to block a client on CloudFront, we can do the following:
        - Use georestriction to restrict the country from where traffic is coming from
        - Use WAF IP Address filtering on the CloudFront distribution

