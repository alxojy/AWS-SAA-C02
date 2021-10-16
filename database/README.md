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


























