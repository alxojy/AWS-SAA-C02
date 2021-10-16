# Compute

## <a href="https://aws.amazon.com/ec2/faqs/">Amazon EC2 FAQ</a>
#### What is Amazon EC2?
- Virtual machine on the cloud
- Boot new server instances in minutes to quickly scale computing requirements

#### How to run systems in EC2?
1. Select/ create AMI(s) (custom AMIs must be bundled & uploaded to S3)
2. Define number of On-Demand instances (limited to quota. to increase, request from Amazon)
3. Call RunInstances API
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
- GPU comput instances for general-purpose computing
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
  - If the instance does not use the credits it receivers, they are stored in its CPU credit balance up to a max threshold

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

#### Why is the limit 5 EIP addresses per region?
Public IPV4 addresses are limited. The limit can be raised by submitting a request

#### Why are there charges when EIP address is not associated with a running instance?
To ensure customers are efficiently using the EIP addresses

#### Elastic Load Balancing (<a href="https://aws.amazon.com/ec2/faqs/#Elastic_Load_Balancing">ELB</a>)
- Distributes incoming traffic across multiple targets including EC2 instances

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

