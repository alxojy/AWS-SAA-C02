# Security, Identity & Compliance
#### Contents
- [AWS Shield](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-shield-faq)
- [AWS WAF](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-web-application-firewall-waf-faq)
- [Amazon GuardDuty](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#amazon-guardduty-faq)
- [AWS Certificate Manager (ACM)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-acm-faq)
- [AWS Key Management Service (AWS KMS)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-kms-faq)
- [AWS Secrets Manager](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-secrets-manager-faq)
- [AWS Single Sign-On](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-sso-faq)
- [AWS Identity and Access Management (IAM)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-iam-faq)
- [Amazon Inspector](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#amazon-inspector-faq)
- [AWS Directory Service](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-directory-service-faq)

## [AWS Shield FAQ](https://aws.amazon.com/shield/faqs/)
#### What is AWS Shield?
Managed service that provides protection against DDoS

#### What is AWS Shield Standard?
Provides protection for all AWS customers against common & most frequently occuring layer 3 & 4 attacks such as SYN/UDP floods, reflection attacks and others

#### What is AWS Shield Advanced?
- Provides enhanced protections for your applications running on protected EC2, ELB, CloudFront, Global Accelerator & Route53 resources
- Provides always-on, flow-based monitoring of network traffic & active application monitoring to provide near real-time notifications of suspected DDoS incidents

#### Can AWS Shield be used to protect websites not hosted on AWS?
Yes. AWS Shield is integrated with CloudFront which supports custom origins out of AWS

## [AWS Web Application Firewall (WAF) FAQ](https://aws.amazon.com/waf/faqs/)
#### What is AWS WAF?
Protect web applications from attacks by allowing rule configurations that allow, block, monitor web requests based on conditions such as IP addresses, HTTP headers, HTTP body, URI strings, SQL injection & XSS

#### How does AWS WAF protect websites/ applications?
- Tightly integrated with CloudFront, ALB, API Gateway & AppSync
- When using WAF on CluodFront, all rules run in all edge locations located around the world
- Blocked requests are stopped before reaching the web servers
- When using WAF on regional services such as ALB, API Gateway & AppSync, the rules run in region & can be used to protect internet-facing resources & internal resources

#### Can AWS WAF be used to protect websites not hosted on AWS?
Yes. AWS WAF is integrated with CloudFront which supports custom origins out of AWS

#### What types of attacks can AWS WAF stop?
- SQL injection
- XSS
- Create rules to block or rate-limit traffic from specific user agents, IP addresses or requests with specific request headers

#### How to get a history of all AWS WAF API calls made?
Use CloudTrail

## [Amazon GuardDuty FAQ](https://aws.amazon.com/guardduty/faqs/)
#### What is Amazon GuardDuty?
- Offers threat detection to continuously monitor & protect AWS accounts, workloads & data stored in S3
- Analyzes continuous streams of metadata generated & network activity found in CloudTrail events, VPC flow logs & DNS logs
- Uses integrated threat intelligence, anomaly detection & ML to identify threats more accurately

#### Amazon GuardDuty vs Amazon Macie
GuardDuty | Macie
----|----
Broad protection of AWS accounts, workloads & data by helping to identify threats such as attacker reconnaissance, instance compromise, account compromise & bucket compromise | Discover & protect sensitive data in S3 by classifying data, security & access controls on the data

## [AWS ACM FAQ](https://aws.amazon.com/certificate-manager/faqs/)
#### What is ACM?
- Easily provision, manage & deploy public & private SSL/TLS certificates
- SSL/TLS certificates are used to secure network communications & establish the identity of websites over the Internet as well as resources on private networks
- Removes the time consuming manual process of purchasing, uploading & renewing SSL/TLS certificates
- Can quickly request a certificate, deploy it on AWS resources ie. ELB, CloudFront distributions, APIs on API Gateway, Elastic Beanstalk & CloudFormation for public certificates that use email verification

#### What is an SSL/TLS certificate?
- Allow web browsers to identify & establish encrypted network connections to websites using SSL/TLSS protocol
- Certificates are used within a cryptographic system (PKI) that provides a one way party to establish the identity of another party if they both trust a third party known as a certificate authority

#### What are private certificates?
- Identify resources within an organization ie. services, applications, users
- Each endpoint uses a certificate & cryptographic techniques to prove its identity 
- Used by internal API endpoints, web servers, VPN users, IoT devices etc

#### Public vs private certificates
Public | Private
----|----
Identify resources on the public Internet | Identify resources on private networks
Public CAs must meet security standards imposed by the browser & OS | Private CAs are managed by private organizations

## [AWS KMS FAQ](https://aws.amazon.com/kms/faqs/)
#### What is AWS KMS?
- Managed service to easily create & control keys used for cryptographic operations
- Provides a highly available key generation, storage, management & auditing solution to encrypt data

#### Why use AWS KMS?
- To secure data across AWS services
- Centrally manage encryption keys to control access to data
- To verify data using asymmetric keys & create/ manage private keys

#### Key management features available in AWS KMS
- Create symmetric and asymmetric keys where the key material is only ever used within the service
- Create symmetric keys where the key material is generated and used within a custom key store (CloudHSM) under the client's control
- Import own symmetric key material for use within the service
- Create both symmetric and asymmetric data key pairs for local use within applications
- Define which IAM users and roles can manage keys
- Define which IAM users and roles can use keys to encrypt and decrypt data
- Choose to have keys that were generated by the service to be automatically rotated on an annual basis
- Temporarily disable keys so they cannot be used by anyone
- Re-enable disabled keys
- Schedule the deletion of keys that are no longer used
- Audit use of keys by inspecting logs in AWS CloudTrail

#### How does AWS KMS work?
Steps | &nbsp; | Options | &nbsp;
----|----|----|----
&nbsp; | Request the creation of a KMS key | &nbsp; | &nbsp;
&nbsp; | Control the lifecycle of the KMS key as well as who can use/ manage it | &nbsp; | &nbsp;
1 | The key material for a KMS key is generated within HSMs managed by AWS KMS | Import the key material from own key management infrastructure & associate it with a KMS key | Have key material generated & used in a CloudHSM cluster as a part of the custom key store feature in KMS
2 | &nbsp; | KMS key is created | &nbsp;
3 | &nbsp; | Submit data directly to AWS KMS to be signed, verified, encrypted or decrypted using this KMS key | &nbsp;
4 | &nbsp; | Set usage policies on the keys to determine which users can perform which actions under which conditions | &nbsp;

- AWS services & client side toolkits that integrate with KMS use a method known as envelope encryption
- KMS generates data keys used to encrypt each data locally in the AWS service or application
- Data keys are also encrypted under a master key defined in KMS 
- Data keys are not retained or managed by KMS
- For data decryption by the AWS service, the encrypted data key is passed to KMS and decrypted under the master key that was originally encrypted under so the service can then decrypt the data
- AWS service then decrypts the data & returns it in plaintext

| ![](https://jayendrapatil.com/wp-content/uploads/2019/08/key-hierarchy-cmk.png)|
|:----:|
| Envelope encryption |

#### KMS access control
- Manage access to KMS CMKs with key policies
- Use IAM policies with key policies to manage permissions of IAM users and roles
- Use grants with key policies to allow users to delegate their access to others

### Custom key store
#### What is a CMK?
- Combines controls provided by CloudHSM with the integration & ease of use of KMS
- Configure own CloudHSM cluster & authorize KMS to use it as a dedicated key store rather than KMS key store
- Provides the option to manage the lifecycle of KMS keys independently of KMS
- Allows keys to be protected in a single tenant HSM
- Validated to FIP 140-2 level 3
- Provides the ability to immediately remove key material from KMS 
- Fulfils the requirement to audit all use of keys independently of KMS or CloudTrail

#### Do custom key stores affect how keys are managed?
Yes
- Key material cannot be imported into the custom key store
- KMS cannot automatically rotate keys

## [AWS Secrets Manager FAQ](https://aws.amazon.com/secrets-manager/faqs/)
#### What is AWS Secrets Manager?
- Secrets management service to protect access to applications, services & IT resources
- Easily rotate, manage & retrieve database credentials, API keys & other secrets
- Use IAM policies to control which users & applications can access the secrets

#### Secrets Manager vs SSM Parameter Store
Secrets manager | Parameter store
----|----
Can generate random secrets | Cannot generate random secrets
Rotate keys & generate new key/password | Feature unavailable
Billed | Free
Cross account secret sharing via IAM | No cross account secret sharing

## [AWS SSO FAQ](https://aws.amazon.com/single-sign-on/faqs/)
#### What is AWS SSO?
- Centrally manage user identities via SAML IdPs/ enabled cloud applications (ie. Salesforce, Microsoft 365) & custom built in house applications or AD credentials
- Employees no longer have to remember multiple sets of credentials & access URLs to cloud applications
- Assign employees access to AWS accounts managed with AWS Organizations

#### Does AWS SSO support IAM users & groups?
No. SSO does not support IAM currently

#### Does AWS SSO support Amazon Cognito User Pools as an identity source?
No. Amazon Cognito is used to manage identities for customer facing applications and is not a supported identity source in AWS SSO. External identity source(s) can be created via Microsoft AD/ Okta Universal Directory/ Azure AD or other supported IdPs

#### How to control permissions a user gets when they use AWS SSO to access their accounts?
- Can limit the user's permissions by picking a permission set
- Permission sets are a collection of permissions that can be created in SSO, modelling them based on AWS managed policies for job functions or any AWS managed policies

## [AWS IAM FAQ](https://aws.amazon.com/iam/faqs/)
#### What is AWS IAM?
- Control individual & group access to AWS resources
- Assign users security credentials (ie. access keys, passwords, MFA) or temporary credentials to AWS services & resources
- Manage access for federated users & request security credentials with configurable expirations allowing these accounts to access resources without creating an IAM user account for them. Use any identity management solution that supports SAML or AWS SSO
- Allows auditing via CloudTrail
- Enable the AWS account to configure a password rotation policy
- Rotate security credentials regularly
- Provides MFA for privileged users

### IAM user
#### What is a user?
- Unique identity recognized by AWS services & applications
- Can be an individual, system or application requiring access to AWS services

#### Who is able to manage users for an AWS account?
The AWS account holder or individual users that have been granted permissions to place calls to IAM APIs to manage other users

### IAM group
#### What is a group?
- Collection of IAM users to easily manage permissions for a collection of users rather than for each individual user
- Add users to or remove them from a group
- A user can belong to multiple groups
- Groups cannot belong to other groups
- Groups can be granted permissions using access control policies
- Groups do not have security credentials and cannot access web services directly

### IAM role
#### What is an IAM role?
- IAM entity that defines a set of permissions for making AWS service requests
- Not associated with a specific user or group
- Trusted entities assume roles ie. IAM users, applications or AWS services such as EC2

#### What problems do IAM roles solve?
- Allow access delegation with defined permissions to trusted entities without having to share long-term access keys
- IAM roles can be used to delete access to IAM users managed within the account, to IAM users under a different account or to an AWS service ie. EC2

#### IAM role vs IAM user
Role | User
----|----
No credentials | Long term credentials
Cannot make direct requests to AWS services | Used to directly interact with AWS services

#### When to use an IAM user, IAM group or IAM role?
User | Group | Role
----|----|----
Permanent long-term credentials used to directly interact with AWS services | Management convenience to manage the same set of permissions for a set of IAM users | Delegate access within or between AWS accounts

#### Can an IAM role be added to an IAM group?
No

### What are the features of IAM roles for EC2 instances?
- Enables applications running on EC2 to make requests to S3, SQS, SNS without copying the AWS access key(s) to every instance
- Simplifies management & deployment of AWS access keys to EC2 instances
- AWS temporary security credentials are created when making requests from running EC2 instances to AWS services
- Automatic rotation of AWS temporary security credentials
- Granular AWS service permissions for applications running on EC2 instances
- Can be associated with a running instance/ can be changed on a running instance
- 1 IAM role = multiple EC2 instances, 1 EC2 instance = 1 role

#### What are the features of IAM roles for Auto Scaling groups?
All EC2 instances launched in the ASG will have the role as input parameter

### Permissions
#### How do permissions work?
Access control policies are attached to users, groups & roles to assign permissions to AWS resources. By default, IAM users, groups and roles have no permissions; users with sufficient permissions must use a policy to grant the desired permissions

#### [Types of IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)
Managed policies | Inline policies
----|----
Reusable: A single managed policy can be attached to multiple principal entities (ie. users, groups, roles) | Strict 1 to 1 relationship between a policy & identity it's applied to
Central change management: The change is applied to all principal entities that the policy is attached to | The change is only applied to the principal entity it is attached to
Versioning & roll back | 
Delegating permissions management: Allow users in the AWS account to attach & detach policies while maintaining control over the permissions defined in those policies | 
Automatic updates for AWS managed policies

#### How to use temporary security credentials to call AWS service APIs?
- Sign requests with temporary security credentials obtained from AWS Security Token Service (AWS STS)
- Include the "x-amz-security-token" HTTP header for S3
- Include the SecurityToken paramater for other AWS services

## [Amazon Inspector FAQ](https://aws.amazon.com/inspector/faqs/)
#### What is Amazon Inspector?
- Automated security assessment service to test the network accessibility of EC2 instances & the security state of applications running on the instances
- Make security testing a part of development, deployment pipeline & static production systems

## [AWS Directory Service FAQ](https://aws.amazon.com/directoryservice/faqs/)
#### What is AWS Directory Service?
- Managed service providing directories that contain information about an organization including users, groups, computers & other resources
- Designed to reduce management tasks
- Offer high availability directory topology since each directory is deployed across multiple AZs & automatically monitors, detects & replaces domain controllers that fail 

#### What can AWS Directory Service do?
- Easy to setup & run directories in the cloud
- Connect AWS resources with an existing on-premises Microsoft AD
- Once the directory is created, it can be used to manage users & groups, providing SSO to applications & services, create & apply group policies, join EC2 instances to a domain & simplify deployment & management of cloud based Linux & Microsoft Windows workloads
- Use existing corporate credentials to administer AWS resources via IAM

![](https://d1.awsstatic.com/Products/product-name/diagrams/directory_service_howitworks.80bfccbf2f5d1d63558ec3c086aff247147258f1.png)

