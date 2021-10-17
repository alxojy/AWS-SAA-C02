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
#### How secure is data stored in S3?
- By default only resource owners have access to S3 resources they create
- Securely upload/ download data via SSL endpoints using HTTPS protocol
- Server side encryption (SSE) can be configured to encrypt data stored at rest

#### How to control access to data on S3?
Access control to selectively grant permissions to users & groups
- IAM policies
  - Enables organizations with multiple employees to create & manage multiple users under a single AWS account
  - Owners can grant IAM users fine-grained control to their S3 bucket or objects while retaining full control over everything their users do
- Bucket policies
  - Owners can define rules that apply broadly across all requests to their S3 resources such as granting write privileges to a subset of S3 resources
  - Restrict access based on HTTP referrer & IP address
- Access Control Lists (ACLs)
  - Owners can grant specific permissions (ie. READ, WRITE, FULL_CONTROL) to specific users for an individual bucket or object
- Query String Authentication
  - Owners can create a URL to an S3 object which is only valid for a limited time

#### Encryption
- SSE-S3
  - Amazon handles key management & protection 
- SSE-C
  - Amazon performs encryption & decryption while the user manages their own encryption keys used to encrypt objects
- SSE-KMS
  - Uses <a href="https://aws.amazon.com/kms/">AWS KMS</a> to manage encryption keys
  - KMS provides an audit trail to see who used the key to access which object & when

#### What is a <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html#types-of-vpc-endpoints-for-s3">VPC endpoint for S3</a>?
Amazon VPC endpoint allows connectivity to S3 over the Amazon global network
Gateway endpoint | Interface endpoint
----|----
Public IP addresses | Private IP addresses from VPC
Does not allow access on-premises | Allow access on-premises
Does not allow access from another region | Allow access from a VPC in another region using VPC peering or AWS Transit Gateway
Not billed | Billed

#### AWS <a href="https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#accessing-elb-apis-from-vpc-without-public-ips">PrivateLink</a> for S3
- Provides private connectivity between S3 & on-premises
- Can provision interface VPC endpoints for S3 in VPC to connect on-premises applications directly to S3 via AWS Direct Connect or AWS VPN
- Public IPs, firewall rules, internet gateway are no longer required

#### Amazon Macie
Uses ML to recognise sensitive data ie. PII & protect against security threats by continously monitoring data & account credentials

### <a href="https://aws.amazon.com/s3/faqs/#Durability_.26_Data_Protection">Durability</a>
#### What is versioning?
- Allows the user to preserve, retrieve and restore every version of every object stored in an S3 bucket
- S3 preserves existing objects whenever a PUT, POST, COPY or DELETE operation on them
- Offers an additional level of protection by providing a means of recovery when customers accidentally overwrite or delete objects

#### How to ensure maximum protection against accidental deletion?
Versioning's MFA delete capability can be used to permanently delete a version of an object

### <a href="https://aws.amazon.com/s3/storage-classes/">S3 storage classes</a>
#### <a href="https://aws.amazon.com/s3/storage-classes/#General_purpose">S3 Standard</a>
- For most use cases
- Low latency & high throughput
- Supports SSL for data in transit & encryption of data at rest

#### <a href="https://aws.amazon.com/s3/faqs/#S3_Intelligent-Tiering">S3 Intelligent Tiering</a>
- Automatically moves data to the most cost effective access tier 
- Used for unknown or changing access patterns
- Frequent & infrequent access tiers have same low latency & high throughput as S3 Standard
- Archive access & deep archive access tiers have same performance as Glacier & Glacier Deep Archive
![s3-intelligent](https://d1.awsstatic.com/product-marketing/S3/How_it_works_diagram_Amazon_S3_Intelligent_Tiering.661d3eed1ef6d91ef168e55c3e697d8686d0c93e.png)

#### <a href="https://aws.amazon.com/s3/faqs/#S3_Standard-Infrequent_Access_.28S3_Standard-IA.29">S3 Standard-Infrequent Access</a>
- For data accessed less frequently but requires rapid access when needed
- Same low latency & high throughput as S3 Standard
- Supports SSL for data in transit & encryption of data at rest
  
#### <a href="https://aws.amazon.com/s3/faqs/#S3_One_Zone-Infrequent_Access_.28S3_One_Zone-IA.29">S3 One Zone-Infrequent Access</a>
- Store objects in a single AZ (20% less cost than S3 IA)
- Same features as S3-IA

#### <a href="https://aws.amazon.com/s3/faqs/#Amazon_S3_Glacier">S3 Glacier</a>
- For data archiving
- Configurable retrieval times
  - Expedited: 1-5 minutes
  - Standard: 3-5 hours
  - Bulk: 5-12 hours
- Supports SSL for data in transit & encryption of data at rest

#### <a href="https://aws.amazon.com/s3/faqs/#Amazon_S3_Glacier_Deep_Archive">S3 Glacier Deep Archive</a>
- Lowest cost storage class designed for long-term retention
- Retrieval time within 12 hours

#### <a href="https://aws.amazon.com/s3/faqs/#S3_on_Outposts">S3 Outpost</a>
- S3 Object compatibility and bucket management through the S3 SDK
- Designed to durably and redundantly store data on Outposts
- Encryption using SSE-S3 and SSE-C
- Authentication and authorization using IAM, and S3 Access Points
- Transfer data to AWS Regions using AWS DataSync
- S3 Lifecycle expiration actions

#### Performance chart
<div class="lb-tbl lb-tbl-p lb-tbl-header-centered" data-is-sticky-header="false"> 
  <table cellspacing="0" cellpadding="1"> 
   <tbody> 
    <tr> 
     <th>&nbsp;</th> 
     <th style="text-align: center;">S3 Standard</th> 
     <th style="text-align: center;">S3 Intelligent-Tiering<br> </th> 
     <th style="text-align: center;">S3 Standard-IA<br> </th> 
     <th style="text-align: center;">S3 One Zone-IA<br> </th> 
     <th style="text-align: center;">S3 Glacier<br> </th> 
     <th style="text-align: center;">S3 Glacier<br> Deep Archive<br> </th> 
    </tr> 
     <td>Availability Zones</td> 
     <td style="text-align: center;">≥3</td> 
     <td style="text-align: center;">≥3</td> 
     <td style="text-align: center;">≥3</td> 
     <td style="text-align: center;">1</td> 
     <td style="text-align: center;">≥3</td> 
     <td style="text-align: center;">≥3</td> 
    </tr> 
    <tr> 
     <td>Minimum capacity charge per object</td> 
     <td style="text-align: center;">N/A</td> 
     <td style="text-align: center;">N/A</td> 
     <td style="text-align: center;">128KB</td> 
     <td style="text-align: center;">128KB</td> 
     <td style="text-align: center;">40KB</td> 
     <td style="text-align: center;">40KB</td> 
    </tr> 
    <tr> 
     <td>Minimum storage duration charge</td> 
     <td style="text-align: center;">N/A</td> 
     <td style="text-align: center;">N/A</td> 
     <td style="text-align: center;">30 days</td> 
     <td style="text-align: center;">30 days</td> 
     <td style="text-align: center;">90 days</td> 
     <td style="text-align: center;">180 days</td> 
    </tr> 
    <tr> 
     <td>Retrieval charge</td> 
     <td style="text-align: center;">N/A<br> </td> 
     <td style="text-align: center;">N/A<br> </td> 
     <td style="text-align: center;">per GB retrieved<br> </td> 
     <td style="text-align: center;">per GB retrieved</td> 
     <td style="text-align: center;">per GB retrieved</td> 
     <td style="text-align: center;">per GB retrieved</td> 
    </tr> 
    <tr> 
     <td>First byte latency</td> 
     <td style="text-align: center;">milliseconds</td> 
     <td style="text-align: center;">milliseconds</td> 
     <td style="text-align: center;">milliseconds</td> 
     <td style="text-align: center;">milliseconds</td> 
     <td style="text-align: center;">select minutes or hours</td> 
     <td style="text-align: center;">select hours</td> 
    </tr> 
   </tbody> 
  </table> 
 </div>

### Storage management
#### S3 object tags
- Key-value pairs applied to S3 objects
- Enable simple management of S3 storage including controlling access & lifecycle policies to objects tagged with specific key-value pairs

#### S3 object lock
- Prevents an object version from being deleted or overwritten for a fixed amount of time (retain until dates) or indefinitely (legal hold prevents an object version from being modified until it is explicitly removed)
- Used if regulatory requirements specify that data must be WORM protected
- Two modes
  - Governance: only AWS accounts with specific IAM permissions are able to remove WORM protection from an object version
  - Compliance: WORM protection cannot be removed by any user, including the root user

#### <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/cloudwatch-monitoring.html">S3 CloudWatch metrics</a>
- Enable generation of 1 minute CloudWatch request metrics for S3 bucket
- Configure filters for metrics using a prefix/ object tag or access point

#### S3 lifecycle management
Provides the ability to define the lifecycle of the object & migrate objects from 1 storage class to another
![](https://docs.aws.amazon.com/AmazonS3/latest/userguide/images/lifecycle-transitions-v2.png)

### Analytics
- #### <a href="https://github.com/alxojy/AWS-SAA-C02/tree/main/analytics#athena-faq">Amazon Athena</a>
- #### <a href="https://github.com/alxojy/AWS-SAA-C02/tree/main/database#what-is-redshift-spectrum">Amazon Redshift Spectrum</a>



#### <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html">Multipart upload</a>
- Recommended for objects larger than 100MB
- Required for objects larger than 5GB
























