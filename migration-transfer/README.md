# Migration & Transfer
#### Contents
- [AWS DataSync](https://github.com/alxojy/AWS-SAA-C02/tree/main/migration-transfer#aws-datasync)
- [AWS Migration Hub]()
- [AWS Server Migration Service (SMS)]()
- [AWS Database Migration Service (DMS)]()
- [AWS Transfer Family]()
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
- Integrates tools such as AWS Application Migration Service, AWS Server Migration Service, AWS Database Migration Service into 1 single tool

## [AWS Snowball FAQ](https://aws.amazon.com/snowball/faqs/)
#### What is AWS Snowball?
- Device to transfer TBs or PBs of data out of premises to AWS
- Operates with Snowball Edge devices
- Once the device arrives, the user has to connect it to their local network & set the IP address (manually or automatically with DHCP)
- Limited to migration in a single AWS region. For cross region migration, use S3 Cross-Region replication
- Encryption is done on the Snowball device while the encryption keys are managed by KMS

#### How to transfer data to Snowball Edge?
- Transfer data from local sources to Snowball via an S3-compatible endpoint or NFS file interface
