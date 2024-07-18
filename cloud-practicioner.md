# Cloud Computing

Cloud computing is the on demand delivery of IT resources over the internet with pay-as-you-go pricing.

- Resources you need, when you need.
- Pay for the resources you use.
- Scale up or down as needed.

## Deployment Models

- Cloud based deployment:
  - all parts of the application are in the cloud.
  - low level infrastructure or high level services.
- On-premises deployment:
  - known as private cloud.
  - uses virtualization and resource management tools.
- Hybrid deployment:
  - connects cloud and on-premises resources.

## Benefits of cloud computing

- Trade capital expense for variable expense.
- Benefit from massive economies of scale.
- Stop guessing capacity.
- Increase speed and agility.
- Stop spending money running and maintaining data centers.
- Go global in minutes.

## Computing

### EC2

- Elastic Compute Cloud.
- Virtual servers in the cloud.
- You can launch instances with a variety of operating systems.
- You can stop, start, terminate, and monitor instances.

## Global Infrastructure

- Regions: geographical areas.
- Availability Zones: data centers in a region.
- Edge Locations: endpoints for AWS which are used for caching content.
- Cloudfront: content delivery network (CDN) service.
- Deploy infrastructure in at least 2 availability zones.
- AWS Outposts: bring AWS infrastructure on-premises.

### How to provision resources

- Everything in AWS is an API call.
- API: Application Programming Interface.
- Example: launch an EC2 instance
- Options:

  - AWS Management Console.
  - AWS Command Line Interface.
  - AWS SDKs.
  - Other tools like AWS CloudFormation.

- Elastic Beanstalk: deploy and manage applications.

  - provide code and configuration settings.
  - Elastic Beanstalk handles the deployment, adjusts capacity, load balancing, scaling, and monitoring.

- AWS CloudFormation: create templates to describe resources.
  - create and provision resources.
  - Infrastructure as Code.

## Networking

### VPC

- Virtual Private Cloud.
- Isolated section of the cloud.
- The public and private grouping of resources are known as subnets and they are ranges of IP addresses in your VPC.
- Own private network in the cloud.

Public traffic goes through the internet gateway into the VPC.
Internet Gateway -> Elastic Load Balancer -> EC2 instances.

Virtual Private Gateway - to connect to private resources.

AWS Direct Connect - dedicated network connection from on-premises to AWS.

Nothing can be accessed from the internet by default in a VPC.

IGW -> can access Public Subnet. Subnets can also control traffic permissions.
Every packet that crosses a subnet boundary is checked by a network access control list (NACL).
Security Groups protect the EC2 instances.

Network Access Control List (NACL) - stateless and allows all inbound and outbound traffic.
Security Groups - stateful, allow or deny traffic.

### Route 53

- Domain Name System (DNS) service.
- DNS translates domain names to IP addresses.
- Route 53 is a scalable and highly available service.
- Can route traffic based ou routing policies.
  - Latency based routing
  - Geolocation DNS
  - Geoproximity routing
  - Weighted round robin
- Can use it to register domain names.

## Storage

### EBS

- Elastic Block Store.
- Block storage for EC2 instances.
- Can be detached and reattached to other instances.
- Can be used to create snapshots.
- Snapshots are incremental backups.
- Single AZ.

### S3

- Simple Storage Service.
- Object storage.
- Buckets are containers for objects.
- Objects are files with metadata (a key-value pair).
- Objects can be up to 5TB.
- S3 is a universal namespace.

### EFS

- Elastic File System.
- Network file system.
- Can be shared across multiple instances.
- Can be accessed by multiple instances at the same time.
- Scalable storage.
- Regional service.

### RDS

- Relational Database Service.
- Managed database service.
- Supports multiple database engines.
- Automated backups.
- Read replicas.
