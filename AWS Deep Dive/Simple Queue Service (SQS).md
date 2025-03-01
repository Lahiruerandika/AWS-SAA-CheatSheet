# SQS - Simple Queue Service

## Integration and Messaging

- Deploying multiple applications will inevitable result in the necessity of a communication layer between them
- There are 2 types of integration communication patterns:
    - Synchronous communication
    - Asynchronous communication
- Application decoupling models:
    - SQS: queue model
    - SNS: pub/sub model
    - Kinesis: real-time streaming model

## SQS - Standard Queue

- Oldest offering on AWS (over 10 years old)
- Fully managed service, used to decouple applications
- Attributes:
    - Unlimited throughput, unlimited number of messages in the queue
    - Each message is short leaved: default retention period is 4 days, maximum is 14 days
    - Low latency: <10 ms on publish and receive
    - Limitation for message size: maximum size of a message is 256KB
- SQS Standard Queue can have duplicate messages (at least once delivery)
- It also can have out of order messages (best effort ordering)

### SQS Standard -  Producing Messages

- Producers send messages to the queue using the SDK (SendMessage API)
- The message is persisted on the queue until a consumer deletes it
- Message retention: default 4 days, up to 14 days
- SQS standard has unlimited throughput

### SQS Standard - Consuming messages

- Consumers are applications (running on EC2 instances, other servers or AWS Lambda)
- Consumers poll the queue for messages (they can receive up to 10 messages at a time)
- After the messages are processed the consumers delete the messages from the queue using DeleteMessage API
- Multiple consumers:
    - Consumers receive the messages in parallel
    - Each consumer consumes a fraction of the number of the messages sent
    - We can scale the number of the consumers based on the throughput of processing
- SQS with Auto Scaling Group:
    - We can scale based on the **ApproximateNumberOfMessages** metric by creating a CloudWatch alarm