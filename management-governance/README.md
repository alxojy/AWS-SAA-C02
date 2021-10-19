# Management & Governance
#### Contents
- [AWS Organizations](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#aws-organizations-faq)
- [AWS Resource Access Manager]()
- [AWS Trusted Advisor]()
- [AWS Config]()
- [AWS CloudWatch]()
- [AWS CloudTrail]()
- [AWS Systems Manager]()
- [AWS Auto Scaling]()
- [AWS Backup](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#aws-backup-faq)
- [AWS CloudFormation]()
- [Amazon EventBridge (Amazon CloudWatch Events)]()

## [AWS Organizations FAQ](https://aws.amazon.com/organizations/faqs/)
#### What is AWS Organizations?
- Centrally govern acess to AWS services, resources & regions
- Automate AWS account creation & management, and provision resources with AWS CloudFormation stacks
- Maintain a secure environment with policies & management of AWS security services
- Centrally manage policies across multiple AWS accounts
- Audit environment for compliance
- View & manage costs with consolidated billing
- Configure AWS services across multiple accounts

#### What types of policies does AWS Organizations support?
- Backup policies—requires backups on a specified cadence using AWS Backup
- Tag policies—defines tag keys & allowed values
- AI service opt-out policies—control how AI services store or use content from the organization
- Service Control Policies (SCPs)—define & enforce the actions that IAM users, groups & roles can perform in the accounts to which the SCP is applied

```javascript
// Example SCP
{ 
 "Version":"2012-10-17", 
 "Statement":[ 
   { 
   "Effect":"Allow", 
   "Action":["EC2:*","S3:*"], 
   "Resource":"*" 
   } 
 ] 
}
```

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
