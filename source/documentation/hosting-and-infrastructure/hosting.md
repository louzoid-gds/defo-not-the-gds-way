# How to host a service

At GDS you should use the following cloud platforms to host your service:

* [GOV.UK Platform as a Service (PaaS)](https://cloud.service.gov.uk) to manage deployment of apps and services
* [Amazon Web Services (AWS)](https://aws.amazon.com) for scalable computing, storage and deployment services

We follow the [Government Cloud First policy](https://www.gov.uk/guidance/government-cloud-first-policy) and use Platform as a Service (PaaS) and Infrastructure as a Service (IaaS) solutions to host our services rather than using our own hardware.

Our choice of cloud platforms:

* are highly scalable and available to meet the needs of service users
* have automated tools for GDS administrators to manage their environments

Please read the [Service Manual](https://www.gov.uk/service-manual/technology/deciding-how-to-host-your-service) for more information on how to host your service.

## Consider vendor switching costs

AWS has a large number of available services. Some services such as compute capacity, email and file storage, are common to other providers like Microsoft Azure and Google Cloud Platform. Other services are specific to AWS.

You should be aware that it’s generally easier, quicker and cheaper to switch from common AWS services to other suppliers than from AWS-only services. For example, if you migrate a web API service to another provider it would be harder if the API was built using [Amazon API Gateway](https://aws.amazon.com/api-gateway/) instead of as a traditional web application and then deployed to EC2.

A good use of a less common service would be to use a Lambda function to ship [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) activity logs to a log provider such as Logit. It wouldn’t make sense to rewrite a Lambda function to run on EC2 hardware because this wouldn’t reduce your switching costs.

Core AWS services that are common with its biggest competitors include:

  * [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/)
  * [Networking Products with AWS](https://aws.amazon.com/products/networking/)
  * [Amazon Elastic Block Store (EBS)](https://aws.amazon.com/ebs/) and [Amazon S3](https://aws.amazon.com/s3/)
  * [Amazon Relational Database Service (RDS)](https://aws.amazon.com/rds/)

Less common Amazon Web Services include:

  * [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
  * [AWS Directory Service for Microsoft Active Directory](https://aws.amazon.com/directoryservice/)
  * [Amazon CloudFront](https://aws.amazon.com/cloudfront/)
  * [Amazon DynamoDB](https://aws.amazon.com/dynamodb/)
  * [AWS Lambda](https://aws.amazon.com/lambda/)
  * [Amazon Simple Notification Service (SNS)](https://aws.amazon.com/sns/)
  * [Amazon Simple Queue Service (SQS)](https://aws.amazon.com/sqs/)

## Future platform

Reliability Engineering is working on an Alpha project to provide GDS apps with a common infrastructure platform built and operated using [Kubernetes](https://kubernetes.io/). The new platform will operate in parallel with [GOV.UK PaaS](https://www.cloud.service.gov.uk/).

If you're starting a new project or application contact Reliability Engineering by email using [reliability-engineering@digital.cabinet-office.gov.uk](mailto:reliability-engineering@digital.cabinet-office.gov.uk) or using the [#reliability-eng Slack channel](https://gds.slack.com/messages/CAD6NP598/#) about your needs before standing up new infrastructure.