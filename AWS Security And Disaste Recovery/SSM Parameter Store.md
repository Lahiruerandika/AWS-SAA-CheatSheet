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
