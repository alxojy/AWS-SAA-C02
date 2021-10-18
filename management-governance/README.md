# Management & Governance
#### Contents
- [AWS Organizations]()
- [AWS Resource Access Manager]()
- [AWS Trusted Advisor]()
- [AWS Config]()
- [AWS CloudWatch]()
- [AWS CloudTrail]()
- [AWS Systems Manager]()
- [AWS Auto Scaling]()
- [AWS Backup]()
- [AWS CloudFormation]()
- [Amazon EventBridge (Amazon CloudWatch Events)]()

## [AWS Backup FAQ](https://aws.amazon.com/backup/faqs/)
#### What is AWS Backup?
- Centralized backup service to backup application data across AWS services in the AWS Cloud
- Provides backup scheduling, retention management & backup monitoring
- Supports existing backup functionality provided by EBS volumes, RDS databases, EC2 instances, EFS file systems, Amazon FSx, DynamoDB tables, Storage Gateway 

*Note: Storage Gateway can be used to backup on-premises Storage Gateway volumes*

#### Why use AWS Backup?
Building & managing own backup workflows across all applications in a compliant & consistent manner is complex & costly

#### How does AWS Backup work?
- Create a backup policy called a backup plan which defines parameters such as how frequently to backup resources & how long to store backups
- Assign resources to backup plans & AWS Backup will automatically backup those resources & manage backup retention
