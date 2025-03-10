# API Gateway

- Allows us to create REST APIs which are accessible by the clients
- AWS Lambda + API Gateway: No infrastructure to manage
- API Gateway provides support for WebSocket Protocol
- It handles API versioning (v1, v2, etc.)
- It handles different environment (dev, tets, prod)
- It handles security (authentication and authorization)
- It can create API keys, handles request throttling
- Supports common standards: Swagger / Open API
- It can transform and validate requests and responses
- We can generate SDK and API specifications
- We can cache API responses

## API Gateway - Integrations

- Lambda Functions
    - It can invoke Lambda functions
    - Easy way to expose REST API backed by AWS Lambda
- HTTP
    - Exposes HTTP endpoints in the back-end. Example: internal HTTP API on premise, Application Load Balancer, etc. By this we can add features like rate limiting, user authentication, API keys to existing back-ends
- AWS Service
    - We can expose any AWS API through API Gateway, examples: API for starting a Step Function workflow, API for posting a message to SQS

## Endpoint Types

- Edge-Optimized (default): for global clients
    - Requests are routed through the CloudFormation Edge locations
    - The API Gateway still lives in only one region
- Regional:
    - For clients within the same region
    - Could manually be combined with CloudFront having more control over caching strategies and distributions
- Private:
    - Can only be accessed from a VPC using an ENI
    - We can use resource policies to define access
