# AWS CLI, SDK, IAM Roles and Policies

- Performing tasks against AWS can be done in several ways
    - Using AWS CLI from a local machine
    - Using AWS CLI on an EC2 machine
    - Using the SDK from a local machine
    - Using the SDK from an EC2 instance
    - Using the AWS Instance Metadata Service for EC2

## AWS CLI Configuration

- In order to use the CLI from a local machine, we must generate access keys. Access keys can be generated from AWS console IAM service
- Access keys are provided as .csv file and they can be downloaded only once
- Set up AWS CLI from terminal:
    ```
    aws configure
    ```
- This command creates 2 files in `/.aws/config` folder: `config` and `credentials`
- A configuration can be invalidated by deleting the access keys or it can be inactivated
