# Management & Governance
#### Contents
- [AWS Organizations](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#aws-organizations-faq)
- [AWS Resource Access Manager](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#aws-resource-access-manager-faq)
- [Amazon Trusted Advisor](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#amazon-trusted-advisor-faq)
- [AWS Config](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#aws-config-faq)
- [AWS CloudWatch](https://github.com/alxojy/AWS-SAA-C02/blob/main/management-governance/README.md#amazon-cloudwatch-faq)
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

## [AWS Resource Access Manager FAQ](https://aws.amazon.com/ram/faqs/)
#### What is AWS Resource Access Manager?
- Securely share resources across AWS accounts within an organization or organizational units (OU) in AWS organizations and with IAM roles & users for supported resource types
- Eliminates the need to provision & manage resources in every account

#### Shareable AWS resources with RAM
[List of shareable resources](https://docs.aws.amazon.com/ram/latest/userguide/shareable.html)

## [Amazon Trusted Advisor FAQ](https://www.amazonaws.cn/en/support/trustedadvisor/faq/)
#### What is Amazon Trusted Advisor?
Inspects AWS environment & makes recommendations for saving money, improving system performance & closing security gaps
![](https://d1.awsstatic.com/support/jp/Trusted%20Advisor%20best%20practice%20checks%20categories.76a13b0b2bf982c874d0d03e6138b7b73e45680c.png)

## [AWS Config FAQ](https://aws.amazon.com/config/faq/)
#### What is AWS Config?
- Fully managed service with resource inventory, configuration history and configuration change notifications to enable security & governance
- Discover existing AWS resources, export a complete inventory of AWS resources with all configuration details & determine how a resource was configured at any point in time
- Enable compliance auditing, security analysis, resource change tracking & troubleshooting

#### What is a Config Rule?
- Represents desired configurations for a resource & is evaluated against configuration changes on the relevent resources
- Assess overall compliance & risk status from a configuration perspective

#### Benefits of AWS Config
- Easy to track resource's configuration
- View continuously updated details of all configuration attributes associated with AWS resources
- Receive SNS notifications for every configuration change

#### AWS Config supported resource types
[List of AWS Config supported resource types](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html#supported-resources)

## [Amazon CloudWatch FAQ](https://aws.amazon.com/cloudwatch/faqs/)
#### What is Amazon CloudWatch?
- Monitoring service for AWS cloud resources & applications running on AWS
- Collect & track metrics
- Collect & monitor log files
- Set alarms

#### What is Amazon CloudWatch logs?
- Monitor & troubleshoot systems & applications using logs in near real time
- Log data can be stored & accessed indefinitely 

#### Resources monitored with CloudWatch
- EC2 instances
- EBS volumes
- ELBs
- Auto Scaling groups
- EMR job flows
- RDS DB instances
- DynamoDB tables
- ElastiCache clusters
- Redshift clusters
- OpsWorks stacks
- Route53 health checks
- SNS topics
- SQS queues
- SWF workflows
- Storage Gateways

#### List of default CloudWatch metrics
[List of default CloudWatch metrics](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html)

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
