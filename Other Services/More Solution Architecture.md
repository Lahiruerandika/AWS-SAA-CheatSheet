# More Solution Architecture

## Event Processing

- SQS + Lambda:
    - Lambda functions pulls the SQS queue, in case there is a problem, the message is put back onto the queue for reprocessing
    - To avoid endless loops in processing, we can set up a deal-letter queue (DLQ)
- SQS FIFO + Lambda:
    - If a message is not processed, it can block the whole queue
    - In order to get around this, we can also set up a DLQ
- SNS + Lambda:
    - In case a message is not processed, the Lambda will retry 3 times
    - We can also set up a DLQ at the Lambda service level
- Fan Out Pattern:
    - Deliver messages to multiple SQS queues
    - In order to achieve this, we can create an SNS topic and create SQS queue subscribers
    - We can combine Fan Out pattern with S3 events
    - We can also create filter to filter out some events and react to only what is needed
    - We can create as many S3 events as we want 
    - If two events are happening on the same object on the same time, there is a possibility that only one event notification is sent. To overcome this we can use versioning

