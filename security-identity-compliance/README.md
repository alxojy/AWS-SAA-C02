# Security, Identity & Compliance
#### Contents
- [AWS Shield](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-shield-faq)
- [AWS WAF](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-web-application-firewall-waf-faq)
- [Amazon GuardDuty](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#amazon-guardduty-faq)
- [AWS Certificate Manager (ACM)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-acm-faq)
- [AWS Key Management Service (AWS KMS)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-kms-faq)
- [AWS Secrets Manager](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-secrets-manager-faq)
- [AWS Single Sign-On](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-sso-faq)
- [AWS Identity and Access Management (IAM)]()
- [Amazon Inspector]()
- [AWS Directory Service]()

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

## [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/faqs/)
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

## [AWS SSO](https://aws.amazon.com/single-sign-on/faqs/)
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





























