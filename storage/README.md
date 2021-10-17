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

#### <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html">Multipart upload</a>
- Recommended for objects larger than 100MB
- Required for objects larger than 5GB
- Advantages
  - Improved throughput: Upload im parallel
  - Quick recovery from network issues: Minimizes impact of restarting a failed upload
  - Pause and resume object uploads

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
#### <a href="https://github.com/alxojy/AWS-SAA-C02/tree/main/analytics#athena-faq">Amazon Athena</a>
#### <a href="https://github.com/alxojy/AWS-SAA-C02/tree/main/database#what-is-redshift-spectrum">Amazon Redshift Spectrum</a>

### Replication
#### What is Amazon S3 Cross Region Replication (<a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html#crr-scenario">CRR</a>)?
- Automatically replicates data between buckets across different regions
- Replication can be at a bucket level, shared prefix level or object level using S3 object tags
- For lower-latency data access in different geographic regions
- For compliance requirements to store copies of data hundreds of miles apart

#### What is Amazon S3 Same Region Replication (SRR)?
- Automatically replicates data between buckets within the same region
- Replication can be set at a bucket level, shared prefix level or object level using S3 object tags
- For compliance requirements by keeping a copy of data in a separate AWS account in the same region 

#### Can 1 bucket be replicated to more than 1 destination bucket?
Yes

#### Is two way replication possible?
Yes

## <a href="https://aws.amazon.com/ebs/faqs/">Amazon EBS FAQ</a>
### <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html">Amazon EBS volume types</a>
#### Solid state drives (<a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html#solid-state-drives">SSD</a>)
Optimized for transactional workloads involving frequent/ random read/ write operations with small I/O size


<table>
  <thead>
   <tr>
     <th/>
      <th colspan="2" align="center" style="text-align: center;">General Purpose SSD</th>
      <th colspan="3" align="center" style="text-align: center;">Provisioned IOPS SSD</th>
   </tr>
  </thead>
  <tbody>
    <tr>
     <td><b>Volume type</b></td>
     <td><code class="code">gp3</code></td>
     <td><code class="code">gp2</code></td>
     <td><code class="code">io2</code>&nbsp;Block Express
     </td>
     <td><code class="code">io2</code>
     </td>
     <td><code class="code">io1</code></td>
    </tr>
    <tr>
       <td><b>Durability</b></td>
       <td>99.8% - 99.9% durability (0.1% - 0.2% annual failure rate)</td>
       <td>99.8% - 99.9% durability (0.1% - 0.2% annual failure rate)</td>
       <td>99.999% durability (0.001% annual failure rate)</td>
       <td>99.999% durability (0.001% annual failure rate)</td>
       <td>99.8% - 99.9% durability (0.1% - 0.2% annual failure rate)</td>
    </tr>
    <tr>
       <td><b>Use cases</b></td>
       <td colspan="2">
          <div class="itemizedlist">
             <ul class="itemizedlist" type="disc">
                <li class="listitem">
                   <p>Low-latency interactive apps</p>
                </li>
                <li class="listitem">
                   <p>Development and test environments</p>
                </li>
             </ul>
          </div>
       </td>
       <td>
          <p>Workloads that require:</p>
          <div class="itemizedlist">
             <ul class="itemizedlist" type="disc">
                <li class="listitem">
                   <p>Sub-millisecond latency</p>
                </li>
                <li class="listitem">
                   <p>Sustained IOPS performance</p>
                </li>
                <li class="listitem">
                   <p>More than 64,000 IOPS or 1,000 MiB/s of throughput</p>
                </li>
             </ul>
          </div>
       </td>
       <td colspan="2">
          <p>Workloads that require:</p>
          <div class="itemizedlist">
             <ul class="itemizedlist" type="disc">
                <li class="listitem">
                   <p>Sustained IOPS performance or more than
                      16,000 IOPS
                   </p>
                </li>
                <li class="listitem">
                   <p>I/O-intensive database workloads</p>
                </li>
             </ul>
          </div>
       </td>
    </tr>
    <tr>
       <td><b>Volume size</b></td>
       <td colspan="2">1 GiB - 16 TiB </td>
       <td>4 GiB - 64 TiB</td>
       <td colspan="2">4 GiB - 16 TiB </td>
    </tr>
    <tr>
       <td><b>Max IOPS per volume</b> (16 KiB I/O)
       </td>
       <td colspan="2">16,000</td>
       <td>256,000</td>
       <td colspan="2">64,000</td>
    </tr>
    <tr>
       <td><b>Max throughput per volume</b></td>
       <td>1,000 MiB/s</td>
       <td>250 MiB/s *</td>
       <td>4,000 MiB/s</td>
       <td colspan="2">1,000 MiB/s</td>
    </tr>
    <tr>
       <td><b>Amazon EBS Multi-attach</b></td>
       <td colspan="2">Not supported</td>
       <td colspan="3">Supported</td>
    </tr>
    <tr>
       <td><b>Boot volume</b></td>
       <td colspan="5">Supported</td>
    </tr>
  </tbody>
</table>

#### Hard disk drives (<a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html#hard-disk-drives">HDD</a>)
Optimized for large streaming workloads that require high throughput
<table id="w652aac27c33c13c19c15b9">
  <thead>
     <tr>
        <th></th>
        <th>Throughput Optimized HDD</th>
        <th>Cold HDD</th>
     </tr>
  </thead>
  <tbody><tr>
     <td><b>Volume type</b></td>
     <td><code class="code">st1</code></td>
     <td><code class="code">sc1</code></td>
  </tr>
  <tr>
     <td><b>Durability</b></td>
     <td>99.8% - 99.9% durability (0.1% - 0.2% annual failure rate)</td>
     <td>99.8% - 99.9% durability (0.1% - 0.2% annual failure rate)</td>
  </tr>
  <tr>
     <td><b>Use cases</b></td>
     <td>
        <div class="itemizedlist">
           <ul class="itemizedlist" type="disc">
              <li class="listitem">
                 <p>Big data</p>
              </li>
              <li class="listitem">
                 <p>Data warehouses</p>
              </li>
              <li class="listitem">
                 <p>Log processing</p>
              </li>
           </ul>
        </div>
     </td>
     <td>
        <div class="itemizedlist">
           <ul class="itemizedlist" type="disc">
              <li class="listitem">
                 <p>Throughput-oriented storage for data that is infrequently accessed</p>
              </li>
              <li class="listitem">
                 <p>Scenarios where the lowest storage cost is important</p>
              </li>
           </ul>
        </div>
     </td>
  </tr>
  <tr>
     <td><b>Volume size</b></td>
     <td>125 GiB - 16 TiB</td>
     <td>125 GiB - 16 TiB </td>
  </tr>
  <tr>
     <td><b>Max IOPS per volume</b> (1 MiB I/O)
     </td>
     <td>500</td>
     <td>250</td>
  </tr>
  <tr>
     <td><b>Max throughput per volume</b></td>
     <td>500 MiB/s</td>
     <td>250 MiB/s</td>
  </tr>
  <tr>
     <td><b>Amazon EBS Multi-attach</b></td>
     <td>Not supported</td>
     <td>Not supported</td>
  </tr>
  <tr>
     <td><b>Boot volume</b></td>
     <td>Not supported</td>
     <td>Not supported</td>
  </tr>
  </tbody>
</table>

### Encryption
#### What is Amazon EBS encryption?
- Offers encryption of EBS data volumes, boot volumes and snapshots
- Encryption at rest supports Amazon-managed keys or keys created & managed using KMS

## <a href="https://aws.amazon.com/efs/faq/">Amazon EFS FAQ</a>
#### What is Amazon Elastic File System?
- Serverless file system that is easy to setup & scale in the cloud
- Accessible to EC2, ECS, EKS, Fargate & Lambda
- Scale from gigabytes to perabytes without needing to provision storage
- Can be accessed by 100s to 100,000s of compute instances at the same time
- Provides a file system interface & file system semantics (ie. strong consistency & file locking) 
- By default, all file system objects are redundantly stored across multiple AZs

#### Use cases
- Big data & analytics
- Media processing workflows
- Content management
- Web serving
- Home directories

#### EFS vs S3 vs EBS
EFS | S3 | EBS
----|----|----
File storage service for Amazon compute & on premises servers | Object storage service | Block level storage 

#### What EC2 instance types & AMIs are compatible with EFS?
EFS is compatible with all Linux-based AMIs for EC2

#### How to load data into a file system?
<a href="https://aws.amazon.com/datasync/">AWS DataSync</a> allows data from existing file systems to be securely synced to EFS
- Works over any network connection including AWS Direct Connect & AWS VPN
- Can be used to copy files between 2 EFS file systems including cross region & cross account file systems

#### How to control access to EFS file system?
- VPC security groups & IAM can be used to control which EC2 instances have access to EFS
- IAM roles can be used to limit access to other AWS accounts
- For on-premises datacenters, AWS Direct Connect or AWS VPN must be installed















