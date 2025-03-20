# SSM Parameter Store

- Used for securely storing configuration and secrets in AWS
- It can have optional encryption using KMS
- Serverless, scalable, durable, easy SDK
- Version tracking of configurations and secrets
- Configuration management using IAM policies
- Notification with CloudWatch events
- Integration with CloudFormation

## SSM Parameter Store Hierarchy

- Example of hierarchy:

    - /my-department/
        - my-app/
            - dev/
                - db-url
                - db-password
            - prod/
                - db-url
                - db-password
        - other-app
    - /other-department

## SSM Tiers

### Standard

- Total number of parameters: 10K
- Max size of a parameter: 4KB
- Pricing: free
- Parameter policies: NO

### Advanced

- Total number of parameters: 100K
- Max size of a parameter: 8KB
- Pricing: 0.05$ per advanced parameter per month
- Parameter policies: YES
