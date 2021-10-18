# Migration & Transfer
#### Contents
- [AWS DataSync](https://github.com/alxojy/AWS-SAA-C02/tree/main/migration-transfer#aws-datasync-faq)
- [AWS Migration Hub](https://github.com/alxojy/AWS-SAA-C02/blob/main/migration-transfer/README.md#aws-migration-hub-faq)
- [AWS Server Migration Service (SMS)](https://github.com/alxojy/AWS-SAA-C02/blob/main/migration-transfer/README.md#aws-server-migration-service-faq)
- [AWS Database Migration Service (DMS)](https://github.com/alxojy/AWS-SAA-C02/blob/main/migration-transfer/README.md#aws-database-migration-service-faq)
- [AWS Transfer Family](https://github.com/alxojy/AWS-SAA-C02/blob/main/migration-transfer/README.md#aws-transfer-family-faq)
- [AWS Snowball](https://github.com/alxojy/AWS-SAA-C02/blob/main/migration-transfer/README.md#aws-snowball-faq)

## [AWS DataSync FAQ](https://aws.amazon.com/datasync/faqs/)
#### What is AWS DataSync?
- Automates & accelerates copying large amounts of data between existing on-premises storage systems & AWS storage services
- Can copy data between NFS, SMB, self managed object storage, Snowcone, S3 buckets including Glacier, EFS, FSx for Windows File Server
![](https://d1.awsstatic.com/aws-datasync-how-it-works-diagram-transfer-data-from-on-premises-to-AWS.348efd1b0f93399ea4edc7b6fd02a86d115b70e4.png)

#### Use cases
- Replicate active datasets
- Disaster recovery for data loss
- Archive rarely accessed data

#### Encryption
- All data are encrypted via TLS
- DataSync also supports default encryption for S3 buckets, EFS data at rest, FSx data at rest & in transit

#### DataSync vs S3 Replication vs S3 Batch Operations vs Snowball
DataSync | S3 Replication | S3 Batch Operations | Snowball
----|----|----|----
On going data distribution, data pipelines & data lake ingest | Continuous replication of data to a specific destination bucket | For large scale operations on S3 objects ie. copy objects, set object tags, ACLs etc | Offline data transfers for customers with network bandwidth constraints 

#### AWS DataSync vs Storage Gateway 
- Use DataSync to **migrate** existing data to S3
- Subsequently use File Gateway configuration on Storage Gateway to **retain access** to the migrated data and for ongoing updates from on-premises file based applications
- Use a combination of DataSync & File Gateway to minimize on-premises infrastructure while connecting on-premises application to cloud storage. After data migration, File Gateway provides on-premises applications with low latency access to the migrated data

#### AWS DataSync vs S3 Transfer Acceleration vs Transfer Family
DataSync | Transfer Acceleration | Transfer Family
----|----|----
To transfer data from existing storage systems to AWS | For high throughput during large file transfers to S3 for applications already integrated with S3 API | SFTP data exchange with third parties

## [AWS Migration Hub FAQ](https://aws.amazon.com/migration-hub/faqs/)
#### What is AWS Migration Hub?
- Collect & view data about on-premises resources & track the progress of those applications during migration to AWS
- Provides a single place to discover existing servers & track the status of each application migration
- Integrates tools such as AWS Application Migration Service, AWS Server Migration Service, AWS Database Migration Service into 1 single service

## [AWS Server Migration Service FAQ](https://aws.amazon.com/server-migration-service/faqs/)
#### What is AWS SMS?
- Incremental, snapshot-based replication & enables cutover windows measured in hours
- Each server volume replicated is saved as a new AMI which can be launched as an EC2 instance
- If using application groupings, SMS will launch the servers in a CloudFormation stack 
- Server volumes are encrypted in transit by TLS

## [AWS Database Migration Service FAQ](https://aws.amazon.com/dms/faqs/)
#### Will AWS DMS convert Oracle PL/SQL and SQL Server T-SQL code to Amazon Aurora or MySQL or PostgreSQL stored procedures?
Yes. Part of DMS is the free AWS Schema Conversion Tool (SCT) that automates the conversion of Oracle PL/SQL and SQL Server T-SQL code to equivalent code in Amazon Aurora or MySQL or PostgreSQL

#### In addition to one-time data migration, can AWS DMS be used for continuous data replication?
Yes. AWS DMS can be used for both one-time migration into RDS and EC2-based databases as well as for continuous data replication. DMS capture changes in the source database & apply them in a transactionally-consistent way to the target. However, for ongoing continuous replication, it is preferable to use Multi-AZ replication for high availability

#### What sources & targets does AWS DMS support?
Either the source or target must reside in RDS or on EC2

#### What sources & targets does AWS Schema Conversion Tool (SCT) support?
It supports a range of database & data warehouse conversions listed below
- Copy a database schema from a source to a target
- Convert a database or data warehouse schema
- Analyze a database to determine the conversion complexity
- Analyze a database to determine any possible restrictions to running on RDS
- Analyze a database to determine if a license downgrade is possible
- Convert embedded SQL code in an application
- Migrate data warehouse data to Amazon Redshift

#### Data migration steps using AWS DMS
1. Create a target database
2. Migrate the database schema
3. Setup the data replication process
4. Initiate the full load & a change data capture & apply
5. Switchover of production environment to the new database once the target database is caught up with the source database

#### Can DMS replicate data from encrypted data sources?
Yes. AWS DMS can read and write from and to encrypted databases

## [AWS Transfer Family FAQ](https://aws.amazon.com/aws-transfer-family/faqs/)
#### What is AWS Transfer Family?
- Offers fully managed support for the transfer of files over SFTP, FTPS and FTP directly into and out of S3 or EFS
- Supports multiple protocols for business to business file transfers so data can easily & securely be exchanged across stakeholders, third party vendors, business partners or customers
- Remove the need to host & manage own file transfer service which includes operating & managing infrastructure, patching servers & monitoring

## [AWS Snowball FAQ](https://aws.amazon.com/snowball/faqs/)
#### What is AWS Snowball?
- Device to transfer TBs or PBs of data out of premises to AWS
- Operates with Snowball Edge devices
- Once the device arrives, the user has to connect it to their local network & set the IP address (manually or automatically with DHCP)
- Limited to migration in a single AWS region. For cross region migration, use S3 Cross-Region replication
- Encryption is done on the Snowball device while the encryption keys are managed by KMS

#### How to transfer data to Snowball Edge?
Transfer data from local sources to Snowball via an S3-compatible endpoint or NFS file interface
