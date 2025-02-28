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