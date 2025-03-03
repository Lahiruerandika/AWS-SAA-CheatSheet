# AWS Config

- Helps with auditing and recording compliance of AWS resources
- Helps record configurations and changes over time
- Provides the ability of storing the configuration data into S3 where it can be analyzed by Athena
- Problems AWS Config Solves:
    - Check if there is unrestricted SSH access to a security group
    - Check if buckets have public access
    - Find out how did an ALB configuration change over time
- We can receive alerts (SNS notifications) for any change
- AWS Config is a per region service, but it can be aggregated across regions and accounts

## AWS Config Resource

- Ability to view the compliance of a resource over time
- Ability to view configuration of a resource over time
- View CloudTrails API calls if enabled

## CloudWatch vs CloudTrail vs Config

- CloudWatch
    - Performance monitoring (metrics, CPU, network, etc.) and dashboards
    - Events and alerting
    - Log aggregation and analysis
- CloudTrail
    - Record API calls made within an account
    - Define trails for specific resources
    - It is a global service
- Config
    - Record configuration changes
    - Evaluate resources against compliance rules
    - Get timeline of changes and compliance
