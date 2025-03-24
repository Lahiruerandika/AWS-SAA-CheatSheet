# Containers in the Cloud

## ECS - Elastic Container service

- ECS is container orchestration service
- ECS helps to run Docker containers and EC2 machines
- ECS is made of:
    - ECS EC2: running ECS tasks an user-provisioned EC2 instances
    - Fargate: running ECS tasks on AWS provisioned compute instances (serverless)
    - EKS: running ECS on AWS powered Kubernetes
    - ECR: Docker Container Registry hosted on AWS
- ECS and Docker are very popular for micro-services
- IAM security and roles are at the task level

### Concepts

- ECS cluster: set of EC2 instances
- ECS service: application definitions running on ECS cluster
- ECS tasks + definition: containers running to create the application
- ECS IAM roles: roles assigned to ECS tasks

## ECS - ALB integration

- Application Load Balancer has a direct integration feature with ECS called port mapping
- This allows us to run multiple instances of the same application on the same EC2 machine
- Use cases:
    - Increase resiliency even if the application is running on one EC2
    - Maximize utilization of CPU cores
    - Ability to perform rolling updates without impacting application uptime


