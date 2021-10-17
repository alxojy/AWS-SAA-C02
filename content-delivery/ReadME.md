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
