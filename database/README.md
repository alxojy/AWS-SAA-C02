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
#### Automated backups vs DB snapshots?
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
- Once a DB instance is associated with the paramter group, it uses it to get all the parameter updates to the group

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
Yes. Data is asynchronous replicated but the amount of time is dependent on the network latency

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
- Improve availability by reducing data base failover times
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



























