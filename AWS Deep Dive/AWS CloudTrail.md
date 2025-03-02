# AWS CloudTrail

- Provides governance, compliance and audit for an AWS account
- CloudTrail is enabled by default
- CloudTrail provides a history of events/API calls made within an AWS account from:
    - AWS Console
    - SDK
    - CLI
    - AWS services
- Logs from CloudTrail can be put into CloudWatch Logs
- If a resource is deleted in AWS, CloudTrail should contain trace of the operation
- CloudTrail records account activity and service events from most AWS services and logs the following records:
    - The identity of the API caller
    - The time of the API call
    - The source IP address of the API caller
    - The request parameters
    - The response elements returned by the AWS service