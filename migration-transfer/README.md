# Migration & Transfer
#### Contents

## [AWS Snowball FAQ](https://aws.amazon.com/snowball/faqs/)
#### What is AWS Snowball?
- Device to transfer TBs or PBs of data out of premises to AWS
- Operates with Snowball Edge devices
- Once the device arrives, the user has to connect it to their local network & set the IP address (manually or automatically with DHCP)
- Limited to migration in a single AWS region. For cross region migration, use S3 Cross-Region replication
- Encryption is done on the Snowball device while the encryption keys are managed by KMS

#### How to transfer data to Snowball Edge?
- Transfer data from local sources to Snowball via an S3-compatible endpoint or NFS file interface
