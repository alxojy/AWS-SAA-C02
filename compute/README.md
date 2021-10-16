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


