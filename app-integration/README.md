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
