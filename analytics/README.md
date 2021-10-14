# Analytics
### <a href="https://aws.amazon.com/athena/faqs/">Athena FAQ</a>
##### What is Athena?
- Run SQL on S3
- Serverless: No infrastructure to manage
- Easy: Works directly with S3. Simply log into Athena Management Console, define schema & query
- Visualization: Easy integration with QuickSight

##### What can Athena do?
- Analyze data
- Run ah-hoc queries with SQL 
- Process unstructured/ semi-structured/ structured data sets

##### How does Athena store table definitions & schema?
- Uses managed Data Catalog to store information & schema about databases & tables created for data stored in S3
- Can upgrade to AWS Glue Data Catalog. Glue crawlers automatically infer schema & partitions. <b>Benefits</b>:
  - Unified Metadata Repo: AWS Glue supports a variety of services including Athena
  - Automatic schema & partition recognition: AWS Glue automatically crawls data sources, identifies data formats, suggests schemas & transformations. Can run periodically to detect availability of new data, changes to data
  - Easy to build pipelines: AWS Glue ETL engine generates Python code that is editable & portable

##### Athena vs EMR vs Redshift overview
Athena | EMR | Redshift
----|----|----
Easiest way to run ad-hoc queries for data in S3 without the need to setup/ manage servers | Simple & cost effective to run highly distributed processing frameworks ie. Hadoop, Spark, Presto | Fastest query performance for enterprise reporting & BI workloads (complex SQL with multiple joins & sub-queries)

##### Athena vs EMR
Athena | EMR
----|----
Simple SQL queries | Custom code to process & analyze large datasets with big data processing frameworks
Limited tasks | Wide variety of data processing tasks (ie. ML, graph analytics, data transformation etc)
Serverless | Requires EC2/ EKS/ Outposts

##### Athena vs Redshift
Athena | Redshift
----|----
Queries directly in S3 | Data from different sources (ie. inventory, financial systems)
Quick queries on web logs to troubleshoot performance issues | Store data for long periods of time to perform complex queries & build sophisticated business reports

##### How to improve query performance?
Convert/ partition data to columnar formats

##### Can Athena query encrypted data in S3?
Yes. Data encrypted using service-side encryption + S3 managed keys/ KMS or client-side encryption + KMS can be queried.

#### <a href="https://aws.amazon.com/glue/faqs/">AWS Glue FAQ</a>
##### What is AWS Glue?
- ETL serverless service
- Data integration for analytics, ML, app development

##### When to use AWS Glue?
- To discover structured & semi-structured data in S3, Redshift & other databases on AWS
- Provides a unified view of data via Glue Data Catalog for ETL, querying, reporting
- Automatically generate Python code for ETL jobs that can be further customized

##### What data sources does AWS Glue support?
- Aurora
- RDS for MySQL, Oracle, PostgreSQL, SQL server
- Redshift
- DynamoDB
- S3
- MySQL, Oracle, Microsoft SQL server, PostgreSQL in VPC on EC2
- Data streams from Kinesis Data Streams, Kafka, MSK
