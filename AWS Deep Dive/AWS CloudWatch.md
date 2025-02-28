# AWS CloudWatch

## AWS CloudWatch Metrics

- CloudWatch provides metrics for every service in AWS
- A **Metric** is a variable to monitor: CPUUtilization, NetworkIn, etc.
- Metrics in CloudWatch belong to **namespaces**
- A **Dimension** is an attribute of a metric, examples: instance id, environment name, etc.
- We can have up to 10 dimensions per metrics
- Metrics have **timestamps**
- We can create CloudWatch dashboards from metrics

## EC2 Details Monitoring

- EC2 instance metrics are gathered every 5 minutes
- We can enable details metrics (for a cost) which will allow gathering every 1 minute
- We can use detailed monitoring if we want more prompt scale for ASG
- Free tier allows to have 10 details monitoring metrics
- EC2 memory usage by default is not pushed to CloudWatch, we should have a custom metric for it

## CloudWatch Custom Metrics

- We have the possibility to send our own custom metrics to CloudWatch
- We can use dimensions (attributes) to segment our metrics
- Metrics resolution by default is 1 minute, but we can have higher resolutions up to 1 second for a higher cost
- We can send metrics by using the **PutMetricsData** API call
- In case of errors we should use exponential back-off

## CloudWatch Dashboards

- Great way to setup dashboards for quick access to key metrics
- Dashboards are global
- Dashboards can include graphs from different regions
- We can change the time zone and time rage for each dashboard
- We can set up automatic refresh (10s, 1m, 2m, 5m, 15m)
- Pricing:
    - 3 dashboards (up to 50 metrics) for free
    - $3/dashboard/month

## CloudWatch Logs

- Applications can send logs to CloudWatch using the SDK
- Also, CloudWatch can collects logs from:
    - Elastic Beanstalk: collection of logs from applications
    - ECS: collections of logs from containers
    - AWS Lambda: collection from functions
    - VPL Flow Logs
    - API Gateway
    - CloudTrail based on filter
    - CloudWatch log agents: from EC2 machines
    - Route53: logs for DNS queries
- CloudWatch logs can be saved to:
    - Batch exporting to S3 for archival
    - Stream logs to ElasticSearch cluster for further analytics
- Log storage architecture:
    - Log groups: arbitrary name, usually representing the name of an application
    - Log stream: instances within application/log files/containers
- We can define a log expiration policy: never expire, 30 days, etc.
- Using the AWS CLI we can tail logs
- To send logs to CloudWatch, we have to make sure the IAM permissions are correct
- Logs can be encrypted at group level using KMS
