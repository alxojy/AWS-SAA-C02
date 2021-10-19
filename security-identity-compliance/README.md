# Security, Identity & Compliance
#### Contents
- [AWS Shield](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-shield-faq)
- [AWS WAF](https://github.com/alxojy/AWS-SAA-C02/blob/main/security-identity-compliance/README.md#aws-waf-faq)
- [Amazon GuardDuty]()
- [AWS Certificate Manager (ACM)]()
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


























