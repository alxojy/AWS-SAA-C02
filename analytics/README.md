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
- Process unstructued/ semi-structured/ structured data sets

##### How does Athena store table definitions & schema?
- Uses managed Data Catalog to store information & schema about databases & tables created for data stored in S3
- Can upgrade to AWS Glue Data Catalog. <b>Benefits</b>:
  - Unified Metadata Repo: AWS Glue supports a variety of services including Athena
  - Automatic schema & partition recognition: AWS Glue automatically crawls data sources, identifies data formats, suggests schemas & transformations
  - Easy to build pipelines: AWS Glue ETL engine generates Python code that is editable & portable

##### Athena vs EMR vs Redshift overview
Athena | EMR | Redshift
----|----|----
Easiest way to run ad-hoc queries for data in S3 without the need to setup/ manage servers | Simple & cost effective to run highly distributed processing frameworks ie. Hadoop, Spark, Presto | Fastest query performance for enterprise reporting & BI workloads (complex SQL with multiple joins & sub-queries)

##### Athena vs EMR

##### Athena vs Redshift
Athena | Redshift
----|----
Queries directly in S3 | Data from different sources (ie. inventory, financial systems)
Quick queries on web logs to troubleshoot performance issues | Store data for long periods of time to perform complex queries & build sophisticated business reports



#### <a href="https://aws.amazon.com/glue/faqs/">AWS Glue FAQ</a>
