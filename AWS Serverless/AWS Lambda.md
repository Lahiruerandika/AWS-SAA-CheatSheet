# AWS Lambda Functions

## Serverless Introduction

- Serverless is a new paradigm in which the developers do not have to manage servers anymore
- Initially Serverless == FaaS (Function as a Service), but now it can mean a lot more
- Serverless was pioneered by AWS Lambda but now the concept also includes anything that is not managed: databases, messaging, storage, etc.
- Serverless does not meant there are no servers, it means that we are not responsible for managing the underlying infrastructure

## Serverless in AWS

- AWS Lambda
- DynamoDB
- AWS Cognito
- AWS API Gateway
- Amazon S3
- AWS SNS and SQS
- AWS Kinesis Data Firehose
- Aurora Serverless
- Step Functions
- Fargate

## AWS Lambda Introduction

- AWS Lambda Functions are virtual functions, which means there are no servers to manage
- There are limited to time - they require short execution times
- They run on-demand - we are only billed when the function is running
- Scaling is automated

## Benefits of Lambda

- Easy pricing
    - Pay per request and compute time
    - Generous free tier: 1 million AWS requests for free and 400K GBs compute time
- Lambda is integrated with the AWS suite of services
- It supports a lot of programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per functions (up to 3GB or RAM)
- Increasing the RAm will also increase the CPU and network
- Supported languages:
    - NodeJS (JavaScript)
    - Python
    - Java
    - C# (.NET Core and PowerShell)
    - Golang
    - Ruby
    - Custom Runtime API (community supported, example Rust)
- **Docker does not run on AWS Lambda!**
