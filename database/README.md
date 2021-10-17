# Database

## <a href="https://aws.amazon.com/rds/faqs/">Amazon RDS FAQ</a>
#### What is Amazon RDS?
- Managed service to setup, operate & scale relational database in the cloud; AWS manages database administration tasks
- Supported databases include Aurora, MySQL, MariaDB, Oracle, SQL Server, PostgreSQL
- Automic backups & keeps the database software up to date
- Easy replication

#### What does Amazon RDS manage?
- Provisioning requested infrastructure capacity
- Database software installation
- Automates common administration tasks ie. performing backups & patching database software
- Synchronous replication across AZs with automatic failover for multi-AZ deployments

#### How to run RDS on-premises
- <a href="https://aws.amazon.com/rds/outposts/">Outposts</a>
- VMware

#### What is a database (DB) instance?
Database environment in the cloud with compute & storage resources specified

#### How to access running DB instance?
Retrieve its endpoint via DB instance description & construct the connection string needed to connect directly with the DB instance

#### Import data into DB instance
<a href="https://aws.amazon.com/dms/faqs/?nc=sn&loc=6">AWS Database Migration Service (DMS)</a> with AWS Schema Conversion Tool (SCT) can migrate data to AWS easily and copy database schemas for homogenous migrations/ convert them for heterogenous migrations

#### What is a maintenence window?
- To control when DB instance modifications, DB engine version upgrades & software patching occurs
- DB instance will be taken offline

#### What is Amazon RDS General Purpose (SSD) storage?
Suitable for database workloads with moderate I/O requirements. It provides predictable performance to meet the needs of most applications

#### What is Amazon RDS Provisioned IOPS (SSD) storage?
Designed to deliver fast, predictable & consistent I/O performance. It is optimized for I/O intensive, OLTP database workloads

### Automated backups & database snapshots
#### Automated backups vs DB snapshots
Automated backups | DB snapshots
----|----
Enables point in time recovery of DB instance (up to most recent restorable time which is usually within the last 5 minutes) | Enables recovery up to the most recent snapshot
Automatically performs a full daily snapshot of data & captures transaction logs | User-initiated 
Backups are retained for 7-35 days | Snapshots are kept until explicitly deleted

#### Are backups automatically enabled?
Yes. By default, RDS enables automated backups of DB instances with a 7 day retention period

#### Where are the automated backups & DB snapshots stored?
S3

### Security
#### What is a DB subnet group?
- Collection of subnets to designate RDS DB instances in a VPC
- Should have at least 1 subnet for every AZ 

#### Encrypting data in transit
- Supported for all RDS engines
- RDS generates an SSL/TLS certificate for each DB instance
- Once an encrypted connection is established, data transferred between the DB instance & application are encrypted during transfer

#### Encrypting data at rest
- Supports encryption at rest for all RDS engines using keys managed using KMS
- Data stored at rest, automated backups, read replicas, snapshots are encrypted
- Encryption can be added to a previously unencrypted DB instance by creating a DB snapshot
- Creating a copy of the snapshot
- Specifying a KMS encryption key
- Restore the encrypted DB instance from the encrypted snapshot

#### How to control permissions the systems & users can take on RDS resources?
- Reference RDS resources in IAM policies applied to users & groups to control their access
- Use tagging to categorize resources & write IAM policies that list the permissions that can be taken on resources with the same tags

#### DB parameter groups
- Custom DB parameter groups can be used to run DB instances with custom-specified engine configuration values
- Once a DB instance is associated with the parameter group, it uses it to get all the parameter updates to the group

#### How to monitor configuration of RDS resources?
<a href="https://aws.amazon.com/config/">AWS Config</a> can be used to continuously record configurations changes to RDS DB instances, subnet groups, snapshots, security groups & event subscriptions

### Multi-AZ deployments
#### What is a Multi-AZ deployment?
- RDS provisions & maintains a synchronous "standby" replica in a different AZ
- Updates to the primary DB are synchronously replicated to the standby
- In the event of failure, RDS automatically fails over to the standby. Failure include
  - Loss of availability in primary AZ
  - Loss of network connectivity to primary
  - Compute unit failure on primary
  - Storage failure on primary  

*Primary: Writes & reads*  
*Standby: Only a replica of the primary DB*

#### Benefits of Multi-AZ deployments
- Safeguards data in the event of a DB instance failure/ loss of availability in the AZ
- User initiated restore operation not required. Failover is automatic
- Impact is limited to the time the automatic failover takes to complete
- I/O activity during backup window is not suspended for the primary DB

#### Can the standby perform read & write operations?
No. For scaling, refer to <a href="https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html">read replicas</a>

#### What happens during Multi-AZ failover?
- RDS flips the CNAME to point to the standby (new primary)
- Typically takes 1-2 minutes

### Read replicas
#### What is a read replica?
![read-replica](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/read-replica.png)|
|:---:|
|Read replica|

#### Common read replica use cases
- Scaling beyond the compute or I/O capacity of a single DB instance for read-heavy DB
- Serving read traffic while the source DB is unavailable
- Business reporting/ data warehousing
- Disaster recovery of the source DB instance

#### Can a read replica be in a different AWS region? 
Yes. Data is asynchronously replicated but the amount of time is dependent on the network latency

#### Can a read replica use a Multi-AZ DB instance deployment as its source?
Yes

#### Can read replicas be configured to be Multi-AZ?
Yes. Read replicas can serve as the primary DB

### Enhanced monitoring
#### Monitored metrics
CPU, memory, file system, disk I/O

### Amazon RDS Proxy
#### What is Amazon RDS Proxy?
Fully managed, highly available, easy to use database proxy that enables applications to 
- Improve scalability by pooling & sharing database connections
- Improve availability by reducing database failover times
- Preserving application connections during failovers
- Improve security by optionally enforcing IAM authentication to databases

#### Use cases
- Applications with unpredictable workloads
  - Gracefully scale by reusing database connections
  - Regulate the number of database connections that are opened

- Applications that frequently open & close database connections
  - Serverless
  - Maintains a pool of database connections to avoid unnecessary stress on database compute & memory for establishing new connections

- Applications that keeps connections open but idle
  - Connections idle to minimize the response time ie. when a customer reengages

- Applications requiring availability through transient failures
  - Automatically routes traffic to a new database instance while preserving application connections

- Improved security 
  - Choice to enforce IAM based authentication
  - Allows centrally managed database credentials through AWS Secrets Manager

## <a href="https://aws.amazon.com/rds/aurora/faqs/">Amazon Aurora FAQ</a>
#### What is Amazon Aurora?
- Managed relational database service that is MySQL & PostgreSQL compatible
- 5x performance of MySQL & 3x performance of PostgreSQL
- 2 copies of the database volume are replicated across 3 AZs = 6 copies total
- Minimum storage: 10GB, maximum storage: 128TB

### Backup & restore
#### DB snapshots
Unlike RDS, there is no performance impact when taking snapshots

#### What is the recovery path if DB fails?
- Amazon Aurora automatically maintains 6 copies of data across 3 AZs & will automatically attempt to recover the DB in a healthy AZ with no data loss
- In the unlikely event that the data is unavailable across all 6 copies, the DB can be restored from a DB snapshot

#### What happens to the automated backups & DB snapshots if the DB instance is deleted?
- A final DB snapshot can be created & retained
- Automated backups are deleted

#### Can snapshots be shared across different regions?
No

### High availability & replication 
#### Fault tolerance to disk failures
- Automatically divides the DB volume in 10GB segments spread across many disks. Each 10GB chunk of database volume is replicated 6 ways, across 3 AZs
- Transparently handle the loss of up to 2 copies of data without affecting DB write availability & 3 copies of data without affecting DB read availability
- Self healing; data blocks & disks are continuously scanned for errors & repaired automatically

#### Amazon Aurora Replicas
- Share the same underlying volume as the primary instance in the same AWS region
- Asynchronous replication for up to 15 replicas
- In-region replication
- Can be promoted to primary in the event of a primary DB instance failure
- For cross-region replication, use MySQL read replicas or native logical replication in each DB engine

#### <a href="https://aws.amazon.com/rds/aurora/global-database/">Aurora Global Database</a>
- For physical replication across different regions
- Supports replication with less than 1s latency
- Uses dedicated infrastructure that can replicate to up to 5 secondary regions
- For low latency global reads & disaster recovery in the event of a region-wide failure

#### What happens during failover & how long does it take?
Failover is automatically handled by Amazon Aurora
- Amazon Aurora Replica in the same/ different AZ
  - Aurora flips the CNAME for the DB instance to point at the healthy replica
  - Completes within 30s
- Aurora Serverless
  - Automatically recreate the DB instance in a different AZ
- No Amazon Aurora Replica/ Aurora Serverless
  - Aurora attempts to create a new DB instance in the same AZ
  - Done in best effort basis & may not succeed (ie. entire AZ is down)    

*Note: Disaster recovery across regions is manual. If the primary region becomes unavailable, a secondary region can be promoted to take on full reads & writes. The application needs to point to the updated promoted region*

#### Amazon Aurora <a href="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-multi-master.html">Multi-Master</a>
![aurora-multi-master](https://d2908q01vomqb2.cloudfront.net/887309d048beef83ad3eabf2a79a64a389ab1c9f/2019/06/11/B.jpg)

### Security
#### Amazon Aurora and VPC
All Aurora DB instances must be created in a VPC

#### Encrypting data in transit
Aurora uses SSL to secure the connection between the DB instance & application

#### Encrypting data at rest
- Aurora allows encrypting the DB using keys managed by KMS
- Data stored, its automated backups, snapshots and replicas in the same cluster are encrypted

#### Can an unencrypted database be encrypted?
No, it is currently not supported. A new DB instance with encryption must be created & the data from the unencrypted database must be migrated to it

### <a href="https://aws.amazon.com/rds/aurora/serverless/">Amazon Aurora Serverless</a>
#### What is Amazon Aurora serverless?
- Automatically starts up, shuts down & scales capacity based on the application's needs
- Runs the database in the cloud without managing the database capacity
- High scalable; scale from 100s to 100,000s of transactions in less than 1s
- Highly available with features such as Global Database, Multi-AZ, read replicas, cloning
- Used for variable/ unpredictable workloads

#### How to migrate an existing Aurora DB cluster to Aurora Serverless?
Restore a snapshot taken from an existing Aurora provisioned cluster into an Aurora Serverless DB cluster

#### How to connect to an Aurora Serverless DB cluster?
It can be accessed from within a client application running in the same VPC. The Aurora Serverless DB cluster cannot be given a public IP address

### <a href="https://aws.amazon.com/rds/aurora/parallel-query/">Amazon Aurora Parallel Query</a>
#### What is Amazon Aurora Parallel Query?
Distribute computational load of a single query across 1000s of CPUs in Aurora's storage layer

#### Uses cases
Analytical workloads requiring fresh data & good query performance

## <a href="https://aws.amazon.com/dynamodb/faqs/">Amazon DynamoDB FAQ</a>
#### What is Amazon DynamoDB?
- Managed nonrelational (NoSQL) database service
- AWS handles hardward provisioning, setup & configuration, throughput capacity planning, replication, software patching, cluster scaling
- Synchronously replicates data across 3 facilities in an AWS region

#### Consistency model
- Eventually consistent reads 
  - Might not reflect the results of a recently completed write
  - Maximizes read throughput
- Strongly consistent reads
  - Returns a result that reflects all writes that received a successful response before the read
- ACID

#### <a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.html">DynamoDB Auto Scaling</a>
|![dynamodb-autoscaling](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/images/auto-scaling.png)|
|:---:|
|High-level overview|
1. Create an application auto scaling policy for the DynamoDB table
2. DynamoDB publishes the consumed capacity metrics to Amazon CloudWatch
3. If the table's consume capacity exceeds the target (or falls below the target) for a specified duration, CloudWatch triggers an alarm & notifications are sent with SNS
4. The CloudWatch alarm invokes application auto scaling to evaluate the scaling policy
5. Application auto scaling issues an `UpdateTable` request to adjust the table's provisioned throughput
6. DynamoDB processes the `UpdateTable` request & dynamically adjusts the table's provisioned throughput capacity to reach the target 

## <a href="https://aws.amazon.com/redshift/faqs/">Amazon Redshift FAQ</a>
#### What is Amazon Redshift?
- Cloud data warehouse to analyze data using SQL & BI tools
- Run analytic queries against structured & semi-structued data
- Queries are distributed & parallelized across multiple physical resources in a single AZ
- Uses replication & continuous backups for availability & failures

#### What is Redshift Spectrum?
- Run SQL queries directly against exabytes of unstructed data in S3 data lakes with no loading/ ETL required
- Suitable for running infrequent queries on cold data in an integrated way from the Redshift cluster

#### How does Amazon Redshift performance compare to most on-premises data warehousing & analytics databases?
- Columnar data storage
- Advanced compression
- Massively parallel processing
- Redshift Spectrum
- Scalability

#### Data sources
- S3
- RDS
- DynamoDB
- EMR
- AWS Glue
- AWS Data Pipeline

#### Security
- Access: IAM, identity federation for single sign on (SSO), MFA, column-level access control, VPC 
- Encryption: SSL, AES-256, KMS

#### What happens to the data warehouse cluster if it supports an AZ outage?
- Redshift automatically moves the cluster to another AZ without any data loss
- Must enable relocation capability in the cluster configuration settings

#### Data backups
- Data are replicated within the data warehouse cluster & backed up to S3
- Redshift attempts to maintain at least 3 copies of data
- Automated backups are retained for 1-35 days

## <a href="https://aws.amazon.com/elasticache/faqs/">Amazon ElastiCache FAQ</a>
#### What is Amazon ElastiCache?
- In-memory caching to improve latency & throughput for read-heavy application workloads
- AWS automates failure detection, recovery & software patching
- Provides detailed monitoring metrics

#### Amazon ElastiCache & VPC
- ElastiCache could be placed in a VPC when running a public-facing web application while still maintaining non-publicly accessible backend servers in a private subnet
- Public-facing subnets could be created for webservers that require access to the Internet
- Backend infrastructure including RDS instances & ElastiCache clusters should be placed in private-facing subnets 

#### Types of caching
- Memcached
- Redis
