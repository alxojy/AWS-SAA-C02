# Content Delivery
#### Contents
- [Amazon API Gateway](https://github.com/alxojy/AWS-SAA-C02/blob/main/content-delivery/ReadME.md#amazon-api-gateway-faq)
- [Amazon Route53](https://github.com/alxojy/AWS-SAA-C02/tree/main/content-delivery#amazon-route53-faq)
- [Amazon CloudFront](https://github.com/alxojy/AWS-SAA-C02/blob/main/content-delivery/ReadME.md#amazon-cloudfront-faq)
- [AWS Global Accelerator](https://github.com/alxojy/AWS-SAA-C02/tree/main/content-delivery#aws-global-accelerator-faq)

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

## [Amazon CloudFront FAQ](https://aws.amazon.com/cloudfront/faqs/)
#### What is Amazon CloudFront?
- Deliver content with low latency & high data transfer rates to end users using a global network of edge locations
- For static files, store definitive versions of files in one or more origin servers including S3 buckets, EC2 instances or other web servers
- Register origin servers with CloudFront via a simple API call. The API call returns a CloudFront.net domain name 

#### How does Amazon CloudFront speed up a website?
- Uses standard cache control headers set on files to identify static & dynamic content
- Uses global network of edge locations

#### How does Amazon CloudFront enable origin redundancy?
- For every origin added to a CloudFront distribution, a [backup origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html) can be assigned to automatically serve traffic if the primary origin is unaivailable
- When the primary origin returns a HTTP status code configured for failover (ie. 4xx or 5xx)/ CloudFront fails to connect to the primary origin/ the response times out, CloudFront routes the request to a secondary origin in the origin group

#### Can a zone apex (naked domain name) point to a CloudFront distribution?
Yes. By using Route53, an Alias record can be configured to map the zone apex to the CloudFront distribution. Route53 responds to each request for an Alias record with the right IP address(es) for the CloudFront distribution

### Edge locations
#### What is CloudFront regional edge cache?
The regional edge caches are located between the origin web server & global edge locations to improve performance for viewers while lowering the operational burden & cost of scaling origin resources

#### How does regional edge cache work?
Regional edge caches have a larger cache width than any individual edge location so objects remain in the cache longer at the nearest regional edge caches. This keeps more of the content closer to the viewers reducing the need for CloudFront to go back to the origin webserver

#### Can CloudFront only server content to specified countries?
Yes. Geo Restriction feature allows clients to specify a list of countries in which users can/ cannot access the content. CloudFront responds to a request from a restricted country with a HTTP status code 403 (Forbidden)

#### How to serve a custom error message?
Custom error messages (ie. HTML file or .jpg image) can be configured to return with HTTP 4xx or 5xx error responses

#### How to remove an item from CloudFront edge locations?
- Delete the file from the origin & after the expiration period defined in the HTTP header, it will be removed
- Invalidation API can be used to remove the object from all CloudFront edge locations for offensive content

### Security
#### Does CloudFront integrate with ACM?
Yes. SSL/TLS certificates can be associated with CloudFront distributions within minutes. Simply provision a certificate using ACM & deploy it to the CloudFront distribution

#### How to safeguard web applications delivered via CloudFront from DDoS?
AWS Shield Standard is integrated into CloudFront at no additional cost. AWS Shield is a managed service that provides protection against SYN/UDP (layer 3 & 4) flood, reflection attacks and others

#### How to protect web applications delivered via CloudFront?
Integrate CloudFront distribution with [AWS WAF](https://aws.amazon.com/waf/) which is a web application firewall that allows rules to be configured based on IP addresses, HTTP headers and custom URI strings

### Logging
#### Standard logs
- Delivered to S3 buckets within minutes of a viewer request
- Access logs contain detailed information about each request including 
  - The object requested
  - Date and time of the request
  - Edge location serving the request
  - Client IP address 
  - Referrer 
  - User agent 
  - Cookie header  
  - Result type

#### Real-time logs
- Delivered to the data stream of the client's choice in Amazon Kinesis Data Streams within seconds of a viewer request
- Can specify the sampling rate (percentage of requests to receive real-time log records) & specific fields 
- Contains the same detailed information as standard logs

## [AWS Global Accelerator FAQ](https://aws.amazon.com/global-accelerator/faqs/)
#### What is AWS Global Accelerator?
- Networking service to improve availability & performance of applications to global users
- Provides static IP addresses to provide a fixed entry point to applications & eliminates the complexity of managing specific IP addresses for different regions
- Routes user traffic to the optimal endpoint based on performance, changes in application health, user's location & policies configured
- Bring your own IP addresses (limit = 2) via BYOIP

#### When to use AWS Global Accelerator?
- Associate static IP addresses provided by AWS Global Accelerator to regional AWS resources & endpoints ie. NLB, ALB, EC2 instances & EIPs
- Move endpoints between AZs or regions without updating DNS configurations
- Dial traffic up or down for a specific region by configuring a traffic dial percantage for endpoint groups
- Control proportion of traffic directed to each endpoint within an endpoint group by assigning weights
![](https://cloudonaut.io/images/2019/11/global-accelerator.png)

#### How does AWS Global Accelerator work with ELB?
- AWS Global Accelerator relies on ELB to provide load balancing features
- However, while ELB provides load balancing within 1 region, AWS Global Accelerator provides traffic management across multiple regions
- A regional ELB is an ideal target for AWS Global Accelerator to distribute incoming application traffic across backends ie. EC2 instances or ECS tasks within a region
![](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2020/01/24/aga-ip-preservation-alb.png)

#### AWS Global Accelerator vs Amazon CloudFront
Global Accelerator | CloudFront
----|----
Improves performance for applications over TCP or UDP by proxying packets at the edge to applications running in 1 or more regions | Improves performance for cacheable content (ie. images) & dynamic content (ie. dynamic site delivery)

#### How to use AWS Global Accelerator for object storage with Amazon S3?
- [S3 Multi-Region Access Points](https://aws.amazon.com/s3/features/multi-region-access-points/) use Global Accelerator to provide a single global endpoint to access a data set that spans multiple S3 buckets in different AWS regions
- Allows multi-region applications with the same simple architecture used in a single region to run anywhere in the world

#### Benefits of AWS Global Accelerator
- Instant regional failover
  - Automtically checks the health of applications & routes user traffic only to healthy application endpoints
- High availability
  - 2 IPv4 static IP addresses are allocated to an accelerator serviced by independent network zones
  - Networks zones are isolated units with their own physical infrastructure & server static IP addresses from a unique IP subnet
  - If one static IP address becomes unavailable, AWS GA reroutes the client to a healthy static IP address
- Improved performance
  - AWS GA ingresses traffic from the edge location that is closest to the end client through anycast static IP addresses
  - Chooses the optimal AWS region based on the geography of end clients
- Easy manageability
  - The static IP addresses provided by AWS GA are fixed & provide a single entry point to the application
  - Easily move endpoints between AZs or regions without updating the DNS configuration or client facing applications
  - Use cases include A/B testing, application updates & failover simulations
- Fine grained control
  - Set a traffic dial for regional endpoint groups to dial traffic up or down for a specific AWS region

#### Are there benefits of using AWS Global Accelerator in a single AWS region?
Yes
- Leverage AWS globally redundant network to improve application availability 
- Easily move the application between AWS regions without changing the public interface

#### Global Accelerator IP addresses vs EC2 Elastic IP addresses
Both are static
GA IPs | EC2 EIPs
----|----
Associated with 1 or more endpoints - ALB, NLB, EC2 in any number of AWS regions | Tied to a single AWS resource - ELB or EC2 in a single AWS region
Support client generated connections | Support both client & server generated connections
Advertised from AWS network of edge locations | Advertised from a single AWS region
