# Storage

## <a href="https://aws.amazon.com/s3/faqs/">Amazon S3</a>
#### What is Amazon S3?
- Quickly accessible, always available & secure object storage
- Unlimited storage

#### How is S3 data organised?
- When data is stored, a unique object key is assigned to retrieve the data
- Alternatively, S3 object tagging can be used to organize data across S3 buckets & prefixes

#### S3 consistency model
Strong read after write consistency. After a successful write of a new object or overwrite of an existing object, any subsequent read requests immediately receive the latest version of the object

#### Where are data stored?
An AWS region is initially specified for the S3 bucket. For   
- Objects stored across multiple devices spanning at least 3 AZs
  - S3 Standard, Standard-IA, Glacier
- Objects stored redundantly in a single AZ
  - S3 One Zone-IA
- Objects stored on-premises
  - Outpost

#### How to decide which region to store data in?
- Near to customers, data centers or other AWS resources
- Remote from other operations for geographic redundancy
- Addresses specific legal & regulatory requirements
- Reduce storage costs by selecting a cheaper region

### Billing
#### How is S3 charged?
- No data transfer charge for COPY requests within an S3 region
- No data transfer charge between EC2 & S3 in the same region

### Event notification
#### What are S3 event notifications?
- Notifications can be sent in response to actions in S3 ie. PUT, POST, COPY, DELETE
- Can setup triggers to perform actions such as transcoding media files when they are uploaded or processing data files when they're available
- Can create notifications based on object name prefixes & suffixes
- Notifications can be sent via
  - SNS
  - SQS
  - Lambda

### Amazon S3 Transfer Acceleration
#### What is S3 Transfer Acceleration?
- Enables fast, easy & secure file transfers over long distances across the world
- Leverages Amazon's CloudFront's globally distributed AWS Edge Locations
- Data is routed to the S3 bucket via an optimized network path

#### How to use Transfer Acceleration?
- Enable S3 Transfer Acceleration
- Use these endpoints to access the buckets `.s3-accelerate.amazonaws.com` or `.s3-accelerate.dualstack.amazonaws.com`

#### How secure is Transfer Acceleration?
Same security features as S3 such as TCP & access restriction based on client's IP address

#### S3 Transfer Acceleration vs Amazon CloudFront PUT/POST
Transfer Acceleration | CloudFront PUT/POST
----|----
Optimizes TCP & supports higher throughput | For objects smaller than 1GB

#### S3 Transfer Acceleration with AWS Direct Connect
AWS Direct Connect is a private network between on-premise & AWS. Some customers use S3 Transfer Acceleration over the public Internet where network conditions have poor throughput 

### <a href="https://aws.amazon.com/s3/faqs/#Security">Security</a>








#### <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html">Multipart upload</a>
- Recommended for objects larger than 100MB
- Required for objects larger than 5GB
