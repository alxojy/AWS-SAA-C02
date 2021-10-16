# Application Integration

## <a href="https://aws.amazon.com/sns/faqs/">Amazon SNS FAQ</a>
#### What is Amazon SNS?
- Highly scalable, flexible & cost effective notification service
- Pub-sub messaging paradigm: Notifications delivered to clients using a push mechanism

#### Benefits of Amazon SNS
- Instantaneous, push-based delivery
- Simple APIs & easy integration
- Flexible message delivery over multiple transport protocols
- Inexpensive, pay-as-you-go model

#### How does Amazon SNS work?
[Publisher] --updates--> [Topic] --notifies--> [Subscriber]

#### Delivery formats/ transports for receiving notifications
- HTTP/ HTTPS: Subscribers specify a URL as part of the subscription
- Email/ Email-JSON
- SQS
- SMS

#### Security
Publisher & subscribers can use SSL to secure the channel to send & receive messages

#### Reliability
Upon receiving a publish request, SNS stores multiple copies (to disk) of the message across multiple AZs before acknowledging receipt of the request to the sender

## <a href="https://aws.amazon.com/sqs/faqs/">Amazon SQS FAQ</a>
#### What is Amazon SQS?
- Message queue service used by distributed applications to exchange messages through a polling model
- Used to decouple sending & receiving

#### How is Amazon SQS different from Amazon MQ?
SQS | MQ 
----|----
Brand new cloud applications | Move messaging from existing applications to the cloud

#### Does SQS provide message ordering?
Yes. FIFO queues preserve the exact message order

#### Amazon SQS vs Amazon Kinesis Streams
SQS | Kinesis
----|----
Highly scalable hosted queue for storing messages travelling between applications | Real-time processing of streaming big data

#### Which services do Amazon SQS support?
- EC2
- ECS
- Lambda
- S3
- DynamoDB

#### How to handle messages that can't be processed?
- Dead letter queues (<a href="https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html">DLQ</a>) is another SQS queue that can be used to isolate messages after a maximum number of processing attempts for logging & analysis
- CloudWatch alarms can be configured for messages delivered to a DLQ

#### What is a <a href="https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html">visibility timeout</a>?
- Period of time when SQS prevents other consuming applications from receiving & processing a message (when a consumer is processing the message, the visibility timeout prevents the same message from being processed again by other consumers)
- Default: 30s. Min: 0s. Max: 12hours
- Consumer must delete the message from the queue once the message is successfully processed

#### <a href="https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-short-and-long-polling.html#sqs-long-polling">Long polling</a> with SQS
- Reduce the cost of SQS by eliminating the number of empty responses
- Return messages as soon as they become available
- Responses are not immediate

#### How reliable is the data storage in Amazon SQS?
Message queues are stored in multiple AZs

#### Server-side encryption (SSE) for Amazon SQS
- SSE encrypts the body of a message in an SQS queue using keys managed in KMS
- Messages are encrypted immediately after SQS receives them

#### How long can messages be kept in SQS?
- 1 minute to 14 days
- Default: 4 days




















