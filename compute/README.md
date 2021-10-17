# Compute
#### Contents
- [Amazon EC2](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#amazon-ec2-faq)
- [AWS Elastic Beanstalk](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#aws-elastic-beanstalk-faq)
- [AWS ECS](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#amazon-elastic-container-service-faq)
- [AWS Fargate](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#aws-fargate-faq)
- [AWS EKS](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#amazon-eks-faq)
- [ELB](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#elastic-load-balancing-faq)
- [AWS Lambda](https://github.com/alxojy/AWS-SAA-C02/tree/main/compute#aws-lambda-faq)

## <a href="https://aws.amazon.com/ec2/faqs/">Amazon EC2 FAQ</a>
#### What is Amazon EC2?
- Virtual machine on the cloud
- Boot new server instances in minutes to quickly scale computing requirements

#### How to run systems in EC2?
1. Select/ create AMI(s) (custom AMIs must be bundled & uploaded to S3)
2. Define number of On-Demand instances (limited to quota. to increase, request from Amazon)
3. Call `RunInstances` API
4. Launch EC2 instances if successful

#### What is the difference between local instance store vs Amazon EBS?
Instance store | EBS
----|----
Ephemeral storage that only persists during the instance's lifetime | Data persists beyond the lifetime of the instance. Data can be preserved even when the instance is stopped

#### Is Amazon EC2 used with S3?
Yes. EC2 is used jointly with S3 for instances with root devices backed by local instance storage. To execute systems in EC2, developers load their AMIs into S3

### <a href="https://aws.amazon.com/ec2/instance-types/">Instance types</a>
#### <a href="https://aws.amazon.com/ec2/faqs/#Accelerated_Computing_instances">Accelerated Computing instances</a>
- Family of instances which use hardware accelerators or co-processors to perform some functions ie. floating-point number calculation & graphics processing more efficiently

#### Types of Accelerated Computing instances
- GPU compute instances for general-purpose computing
- GPU graphics instances for graphics intensive applications
- FPGA programmable hardware compute instances for advanced scientific workloads

#### <a href="https://aws.amazon.com/ec2/faqs/#Compute_Optimized_instances">Compute Optimized instances</a>
- Designed for applications that benefit from high compute power
- Batch processing, media transcoding, HPC, scientific modelling, ML etc.

#### <a href="https://aws.amazon.com/ec2/faqs/#General_Purpose_instances">General Purpose instances</a>
- Provide a balance of compute, memory & networking resources
- Used for a variety of diverse workloads

#### <a href="https://aws.amazon.com/ec2/faqs/#High_Memory_instances">High Memory instances</a>
- Run large in-memory databases
- Deliver high networking throughput & low-latency using ENA

#### <a href="https://aws.amazon.com/ec2/faqs/#Storage_Optimized_instances">Storage instances</a>
- Workloads the require high sequential read & write access to very large data sets ie. Hadoop distributed computing, massively parallel processing data warehousing, log processing applications
- Deliver tens of thousands of low-latency, random I/O operations per second (IOPS)

#### <a href="https://aws.amazon.com/ec2/instance-types/#Instance_Features">Instance Features</a>
- Burstable performance instances
  - Provide a baseline CPU level with the ability to burst above the baseline
  - If the instance does not use the credits it receives, they are stored in its CPU credit balance up to a max threshold

- Multiple storage options
  - EBS
  - Instance store
  - S3

- Cluster networking (cluster placement group)
  - Low latency networking between instances in the cluster
  - For high performance computing

### Storage on EC2
#### Amazon Elastic Block Storage (<a href="https://aws.amazon.com/ebs/faqs/">EBS</a>)
- Durable block storage that can be attached to a single EC2 instance
- Used for data that requires frequent & granular updates ie. database

#### What happens to the data when a system terminates?
Data stored on EBS can persist after termination by setting the Delete On Terminate flag to "N"

#### <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html">EBS performance</a>
Performance depends on the type of workload & volume type (SSD or HDD)

#### Do volumes need to be unmounted in order to take a snapshot?
No, however snapshots can only capture data that has been written to the EBS volume. In order to ensure consistent snapshots on volumes attached to an instance (including locally cached data), it is recommended to detach the volume, issue the snapshot command & reattach the volume. For EBS volumes serving as root devices, it is recommended to shut down the machine to take a clean snapshot

#### Amazon Elastic File System (<a href="https://aws.amazon.com/efs/faq/">EFS</a>)
- Uses NFS protocol
- Data can be loaded into EFS from EC2 instances or on-premises datacenters
- Can be mounted to 1-1000s of instances including EC2 instances & on-premises server (via AWS Direct Connect)

### Networking and security
#### <a href="https://aws.amazon.com/ec2/faqs/#Enhanced_networking">Enhanced networking</a>
- SR-IOV (Single root I/O virtualization) provides higher I/O performance & lower CPU utilization 
- Provides higher packed per second (PPS) performance
- Supports low latency networking
- Uses ENA

#### Elastic Fabric Adapter (<a href="https://aws.amazon.com/ec2/faqs/#Elastic_Fabric_Adapter_.28EFA.29">EFA</a>)
- Tightly-coupled HPC applications have access to lower & more consistent latency & higher throughput than traditional TCP channels
- Provide all ENA functionalities plus OS bypass that allows applications to communicate directly with the hardware provided reliable transport functionality

#### EFA ENI vs ENA ENI
EFA | ENA 
----|----
ENA functionalities + OS bypass | Traditional IP networking features needed for VPC networking

#### EFA pre-requisite
Can only be attached at launch/ to stopped instances

#### <a href="https://aws.amazon.com/ec2/faqs/#Elastic_IP">Elastic IP</a>
- Public address is associated to the instance until it is stopped/ terminated
- Elastic IP address provides a long lived internet routable endpoint

#### Why is there a limit of 5 EIP addresses per region?
Public IPV4 addresses are limited. The limit can be raised by submitting a request

#### Why are there charges when EIP address is not associated with a running instance?
To ensure customers are efficiently using the EIP addresses

#### Elastic Load Balancing (<a href="https://aws.amazon.com/ec2/faqs/#Elastic_Load_Balancing">ELB</a>)
Distributes incoming traffic across multiple targets including EC2 instances

#### <a href="https://aws.amazon.com/ec2/faqs/#Security">Security</a>
- <a href="https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html">Security groups</a> to control inbound & outbound traffic
- An instance can have up to 5 security groups
- By default, all inbound connections are denied

### Management
#### <a href="https://aws.amazon.com/ec2/faqs/#Amazon_CloudWatch">Amazon CloudWatch</a>
- Receives & provides metrics for all EC2 instances
- CloudWatch metrics can be obtained for 2 weeks including for terminated instances

#### <a href="https://aws.amazon.com/ec2/autoscaling/faqs/">EC2 Auto Scaling</a>
- Fully managed service designed to launch/ terminate EC2 instances automatically (terminate instances when CPU utilization is low vice versa)
- Detect impaired EC2 instances & replace automatically
- Create/ configure EC2 auto scaling groups
- Use CloudWatch to send alarms to trigger scaling activities & ELB to distribute traffic to instances within the auto scaling group
- Instances can span AZs

#### What is target tracking?
- Used to setup dynamic scaling
- Select load metric ie. CPU utilization
- Set the target value
- EC2 auto scaling automatically adjusts the number of EC2 instances needed to maintain the target

#### What happens when the auto scaling group (ASG) is deleted?
The EC2 instances will be terminated and the ASG will be deleted

#### What is a <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html">launch template</a>? 
- Includes information that EC2 needs to launch instances ie. AMI, instance type, security groups etc.
- Launch templates cannot be modified after it's created. To change the launch template, a new one has to be created & attached to the EC2 ASG

#### Does ELB health checks work with ASG?
Yes. EC2 auto scaling works with ALB & NLB

#### How to control access to EC2 auto scaling resources?
EC2 auto scaling integrates with IAM
  - Create users & groups
  - Assign unique security credentials to each user
  - Control each user's permissions to perform tasks using AWS resources
  - Create roles & define users/ services that use them
  - Use existing identities to grant permissions to perform tasks using AWS resources

#### <a href="https://aws.amazon.com/ec2/faqs/#Hibernate">Hibernate</a>
- Quickly start up instances (as opposed to the stop state)
- Used for instances that take a long time for bootstrap scripts to run
- RAM data is moved to the EBS root volume (RAM data is typically deleted for stopped instances)
- An encrypted EBS volume must be attached
- Max: 60 days

### EC2 types
#### On demand
- Pay for compute capacity by the hour/ second with no long term commitments
- Short-term, irregular workloads that cannot be interrupted

#### <a href="https://aws.amazon.com/ec2/faqs/#Reserved_Instances">Reserved instances</a>
- Provides a significant discount for 1 or 3 year commitment
- Reserved instance marketplace is used to sell RIs before the commitment term ends

#### <a href="https://aws.amazon.com/ec2/faqs/#Spot_Instances">Spot instances</a>
- Instances can be interrupted with a 2 minute notification
- To prevent data from being lost, spot instances can be used with hibernation (RAM data stored into EBS volumes) & the instances can resume from where it left off prior to interruption

| ![spot-lifecycle](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/spot_lifecycle.png) |
|:---:|
| Spot instance lifecycle |

## <a href="https://aws.amazon.com/elasticbeanstalk/faqs/">AWS Elastic Beanstalk FAQ</a>
#### What is AWS Elastic Beanstalk?
- Developers can simply upload their application & Elastic Beanstalk automatically handles the deployment details of capacity provisioning, load balancing, auto scaling & application health monitoring
- Developers are freed from deployment-oriented tasks ie. provisioning servers, setting up load balancing, managing scaling

#### When to use AWS Elastic Beanstalk?
When it is needed to deploy & manage the application within minutes in AWS Cloud without any experience

#### What elements can be controlled using AWS Elastic Beanstalk?
- OS selection
- Types of EC2 instances (On-Demand, RI, Spot)
- Available database & storage options
- Login access to EC2 instances
- Running code in more than 1 AZ
- Enabling HTTPS protocol on the load balancer
- Access built-in CloudWatch monitoring & notifications on application health etc
- Adjust server settings & pass environment variables
- Run other application components ie. memory caching
- Access log files without logging in to the application servers

#### What are the underlying services used in AWS Elastic Beanstalk?
EC2, ELB, RDS, Auto scaling, S3, SNS, DynamoDB

#### How to control access?
- Use VPC to make application private
- Use IAM to control access & limit permissions

## <a href="https://aws.amazon.com/ecs/faqs/">Amazon Elastic Container Service FAQ</a>
#### What is Amazon ECS?
- Container management service that supports Docker containers
- Easily run applications on a managed cluster of EC2 instances or using Fargate
- Use simple API calls to launch & stop container-enabled applications, query the state of the cluster & access features ie. security groups, ELB, EBS, IAM roles

#### Does Amazon ECS support applications & services?
Yes. ECS service scheduler can manage long-running applications & services. Service scheduler maintains
- Application availability
- Scaling containers up/ down to meet application's capacity requirements
- Allows traffic distribution across containers using ELB
- Automatically register & deregister containers from associated LB
- Automatically recover unhealthy containers (failed ELB health checks)

#### Does Amazon ECS support dynamic port mapping?
Yes. It's possible to associate a service on ECS to an ALB. The ALB supports a target group that contains a set of instance ports. A dynamic port can be specified in the ECS task definition which gives the container an unused port when it is scheduled on the EC2 instance. The ECS scheduler will automatically add the task to the ALB target group using this port

#### Where to run ECS?
- EC2 instances for compliance & governance requirements
- Fargate without having to provision & manage EC2 instances

#### How does AWS Fargate work with ECS?
With Fargate, the concept of server provisioning, cluster management & orchestration goes away. ECS uses containers provisioned by Fargate to automatically scale, load balance & manage scheduling of the containers for availability

#### Security
- IAM roles can be defined
- EC2 instances use an IAM role to access ECS & ECS tasks use an IAM role to access services & resources

## <a href="https://aws.amazon.com/fargate/faqs/">AWS Fargate FAQ</a>
#### What is AWS Fargate?
- Serverless compute engine for containers that works with ECS & EKS
- Eliminates the need to provision servers & manage clusters
- Supports all container use cases including batch processing, microservices applications, ML

## <a href="https://aws.amazon.com/eks/faqs/">Amazon EKS FAQ</a>
#### What is Amazon Elastic Kubernetes Service (EKS)?
- Easily run Kubernetes on AWS without needing to install & operate Kubernetes control plane or worker nodes
- EKS provisions & scales the Kubernetes control plane across multiple AZs
- Automatically detects & replaces unhealthy control plane nodes
- Provide patching for the control plane
- Can run with Fargate; removing the need to provision & manage servers
- Integrated with ELB, IAM, VPC, CloudTrail

## <a href="https://aws.amazon.com/elasticloadbalancing/faqs/">Elastic Load Balancing FAQ</a>
#### Load balancer overview
Application LB | Network LB | Classic LB
----|----|----
layer 7- HTTP, HTTPS requests | layer 4- TCP, UDP for extreme performance/ low latency | Application built within the EC2 classic network

#### Accessing ELB APIs from VPC without public IPs
- VPC can privately access ELB APIs by creating <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-endpoints.html">VPC endpoints</a>
- VPC endpoints powered by AWS PrivateLink handle the routing between VPC & ELB APIs without an Internet gateway/ NAT gateway/ VPN connection

| ![private-link](https://d1.awsstatic.com/product-marketing/PrivateLink/privatelink_how-it-works.a8ae3df6830296337b30a7c4e75d8eed403eb5d2.png) |
|:---:|
| AWS PrivateLink |

### Application Load Balancer
#### How to use static IP/ PrivateLink on ALB?
- Forward traffic from NLB (which has support for PrivateLink & a static IP address per AZ) to the ALB
- Create an ALB target group, register ALB to it & configure the NLB to forward traffic to the ALB target group

#### Can EC2 instances be configured to only accept traffic from ALB?
Yes

#### Can a security group be configured for the frontend of an ALB?
Yes

#### Can a single ALB handle both HTTP & HTTPS requests?
Yes. Listeners can be added for HTTP port 80 & HTTPS port 443

#### How to get a history of ALB API calls?
Use AWS CloudTrail

#### Does ALB support HTTPS termination?
Yes. SSL certificate has to be installed on the ALB. The certificate is used to terminate the connection & decrypt requests from clients before sending it to the targets

#### What are the steps to get a SSL certificate?
- Use <a href="https://aws.amazon.com/certificate-manager/">AWS Certificate Manager (ACM)</a> to provision an SSL/TLS certificate or
- Obtain the certificate from other sources by creating the certificate request -> getting the certificate request signed by a CA -> uploading the certificate using ACM or IAM

#### ALB & ACM integration
- Simplifies SSL offloading process
- Just request a trusted SSL/TLS certificate & select the ACM certificate to provision it with the ALB

#### ALB rules
- Rules can be configured for each listener on the ALB
- Rules include conditions & corresponding actions if the conditions are satisfied
- Supported conditions
  - Host header
  - Path
  - HTTP headers
  - Methods
  - Query paramters
  - Source IP CIDRs
- Supported actions
  - Redirect
  - Fixed response
  - Authenticate
  - Forward

#### How to protect web applications behind ALB?
##### Integrate with <a href="https://aws.amazon.com/waf/faqs/">WAF</a>        
Web application firewall that protects web applications from attacks by allowing configurations based on IP addresses, HTTP headers, custom URI strings

#### ALB user authentication
##### Amazon Cognito
- Provide flexibility to authenticate via social accounts ie. Google, Facebook etc
- Managing multiple identity providers including OpenID Connect & want to create a single authentication rule in ALB that use Cognito to federate multiple identity providers

### Network Load Balancer
#### Key features available with NLB
- Provides both TCP & UDP load balancing
- Handle millions of requests/sec, sudden volatile traffic patterns & extremely low latencies
- TLS termination
- Preserves the clients' source IP

#### Does NLB support DNS regional & zonal fail-over?
Yes. Route53 health checking & DNS failover features can be used to enhance the availability of the applications running behind NLBs. Using Route53 DNS failover, applications can run in multiple AZs & designate alternate LBs for failover across regions

#### NLB IPs
NLB addresses must be completely controlled by the user or by ELB. This is to ensure that when using EIPs with a NLB, all addresses known to the user's clients do not change

#### Can more than 1 EIP be assigned to the NLB in each subnet?
No. Each associated subnet that a NLB is in, the NLB can only support 1 public/ internet facing IP address

#### Can the internal NLB support more than 1 private IP in each subnet?
No. For each associated subnet that a LB is in, the NLB can only support 1 private IP

#### Benefit of targeting containers behind a NLB with IP addresses instead of instance IDs
- Each container on an instance can have its own security group & does not need to share security rules with other containers
- Can map a container to the IP address of a particular ENI to associate security group(s) per container
- Load balancing using IP addresses allows multiple containers running on an instance to use the same port

#### How to load balance applications distributed across a VPC & on-premises
- If the application runs on targets in a VPC & on-premises, they can be added to the same target group using their IP addresses
- Alternatively, separate load balancers can be used for VPC & on-premises targets

#### Does NLB support TLS termination?
Yes. SSL certificate must be installed on the NLB. The NLB uses this certificate to terminate the connection & decrypt requests from clients before sending them to the targets

### Gateway Load Balancer
#### When to use a Gateway LB compared to NLB or ALB?
- When deploying inline virtual appliances where network traffic is not destined for the Gateway LB itself
- Gateway LB passes all layer 3 traffic through 3rd party appliances, and is invisible to the source & destination of the traffic
- Provides both layer 3 gateway & layer 4 load balancing capabilities
- Does not perform TLS termination or encryption/decryption

### Classic Load Balancer
- Supports load balancing for EC2 instances
- Supports load balancing for HTTP, HTTPS, SSL, TCP
- A security group can be configured for the frontend of the CLB
- Supports SSL termination

## <a href="https://aws.amazon.com/lambda/faqs/">AWS Lambda FAQ</a>
#### What is AWS Lambda?
- Runs code without provisioning/ managing servers
- Serverless computing to build & run applications (server management by AWS)

#### <a href="https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html#intro-core-components-event-sources">AWS Lambda event sources</a>
Examples
  - S3
  - API Gateway
  - SQS
  - EventBridge

#### AWS Lambda vs EC2
Lambda | EC2
----|----
Cannot access infrastructure but easy way to execute code in response to events | Customizable OS, network, security settings & entire software stack
Lambda performs capacity provisioning, monitoring fleet health, applying security patches, code deployment, running web service front end, monitoring, logging | Developers must provision capacity, monitor fleet health & performance, design fault tolerance & scalability

#### How does AWS Lambda secure my code?
Lambda stores code in S3 & encrypts it at rest
