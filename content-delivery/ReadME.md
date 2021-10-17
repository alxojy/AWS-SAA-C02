# Content Delivery
#### Contents

## <a href="https://aws.amazon.com/api-gateway/faqs/">Amazon API Gateway FAQ</a>
#### What is Amazon API Gateway?
- Fully managed service to publish, maintain, monitor & secure APIs
- Can integrate API with backend services such as EC2, ECS, Elastic Beanstalk, code running on Lambda or any web application

#### Why use Amazon API Gateway?
- Metering
  - Define a set of plans, configure throttling & quota limits on a per API key basis
- Security
  - IAM & Amazon Cognito to authorize access to APIs
  - For Lambda, can verify incoming bearer tokens & remove authorization concerns
- Resiliency
  - Manage traffic with throttling to handle traffic spikes
  - Improve performance & latency by caching the output of API calls
- Operations monitoring
  - Monitor metrics through Amazon CloudWatch
  - Access & debug logs in CloudWatch Logs
- Lifecycle management
  - Operate multiple API versions & stages  

#### Types of APIs supported
- HTTP
- REST
- WebSocket

#### How to use API Gateway with VPC?
Proxy requests to backend HTTP/HTTPS resources running in VPC by setting up [Private Integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-private-integration.html) using VPC links

## <a href="https://aws.amazon.com/route53/faqs/">Amazon Route53 FAQ</a>
#### What is a DNS service?
Translates URLs ie. www.example.com into IP addresses

#### What is Amazon Route53?
- DNS, domain name registration & health checking web service
- Combine DNS with health checking services to route traffic to healthy endpoints/ to monitor endpoints
- Routes requests to EC2 instances, ELB, S3 buckets or infrastructure outside of AWS

#### How to control access for Domains on Route53?
IAM manages permissions to who can make changes to DNS records

#### Which DNS record types does Route53 support?
- A (address record)
- AAAA (IPv6 address record)
- Alias (Route53 specific. Usually type A or AAAA. Can map record name ie. example.com to the DNS name for an AWS resource ie. elb123.elb.amazonaws.com. Supports routing traffic to AWS resources including ELB, CloudFront, Elastic Beanstalk, API Gateways, VPC interface endpoints, S3 buckets)
- CNAME 
- CAA
- MX
- NAPTR
- NS
- PTR
- SOA
- SPF
- SRV
- TXT

#### Can multiple IP addresses be associated with a single record?
Yes. Multple IP addresses can be listed for an A record

#### DNS [routing policies](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
Policy | Use cases
----|----
Simple routing | - Route traffic to a single resource <br> - Cannot create multiple records with the same name & type <br> - Can specify multiple IP addresses 
Failover routing | - Route to a different resource when the primary resource is unhealthy <br> - [Active-passive failover](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover-types.html#dns-failover-types-active-passive)
Geolocation | - Routes resources based on the location of the users <br> - Maps IP addresses to locations
Geoproximity | Routes traffic based on location of the users + bias
Latency | Serve requests from the AWS region that provides the lowest latency
Multivalue answer routing | Allows multiple IP addresses + health check of each resource 
Weighted routing | Sends traffic to a resource based on the weight

#### Hosted zone
- A container of records which includes information on how to route traffic for a domain
- Public hosted zone: For routing Internet traffic to resources
- Private hosted zone: For routing traffic within a VPC





































