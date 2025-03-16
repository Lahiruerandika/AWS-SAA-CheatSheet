# AWS Secrets Manager

- Sole purpose: store secrets
- Newer service than the SSM Parameters Store
- Has the capability to force the rotation of secrets every X days
- Has the capability to automate generation of secrets on rotation (uses Lambda for this)
- Secrets manager can be integrated with RDS (MySQL, PostgreSQL, Aurora) to synchronize secrets between databases and secrets manager
- Secrets are encrypted using KMS
- Mostly meant for RDS integration
- Pricing: $0.40 per secret per month / $0.05 per 10K API calls + 30 day free trial
- Stores key-value pairs for secrets

## SSM Parameter Store vs Secrets Manager

### Secrets Manager

- Automatic rotation of secrets with AWS Lambda
- Direct integration with RDS, Redshift, DocumentDB
- KSM encryption is mandatory
- Can integrate with ClouDFormation
- In general a more expensive solution for storing secrets
