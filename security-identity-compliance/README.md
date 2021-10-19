# Security, Identity & Compliance
#### Contents
- [AWS Shield](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-shield-faq)
- [AWS WAF](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-web-application-firewall-waf-faq)
- [Amazon GuardDuty](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#amazon-guardduty-faq)
- [AWS Certificate Manager (ACM)](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-acm-faq)
- [AWS Key Management Service (AWS KMS)]()
- [AWS Secrets Manager]()
- [AWS Single Sign-On]()
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




















































