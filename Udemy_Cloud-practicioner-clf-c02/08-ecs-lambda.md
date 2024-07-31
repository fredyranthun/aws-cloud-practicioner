# Docker

- Docker is a software platform to deploy apps
- Apps are packaged in containers that can run on any OS.
- Apps run the same, regardless of where they run
- Scale containers up and down very quickly (seconds)
- We can have many containers in one EC2 instance
- We can store Docker Images on docker repositories like Docker Hub (public) and Amazon ECR (private)
- Docker is sort of a virtualization technology, but not exactly
- Resources are shared with the host -> many containers on one server
- Infrastructure -> Host OS -> Hypervisor -> Guest OS (VM) -> Apps
- Infrastructure -> Host OS -> Docker Daemon -> Multiple containers

# ECS

- Elastic Container Service
- Launch Docker Containers on AWS
- You must provision and maintain the infrastructure (EC2 Instances)
- AWS takes care of starting and stopping containers
- Has integrations with the Application Load Balancer
- ECS decides which EC2 instance it will use to place the docker container

# Fargate

- Launch Docker Containers on AWS
- Do not need to provision the infrastructure
- Serverless
- AWS just runs containers for you based on CPU / RAM you need
- We do not manage EC2 Instances

# ECR

- Elastic Container Registry
- Private Docker Registry on AWS
- Can be run by ECS or Fargate
- E.g.: Fargate use the images on ECR to create the containers

# Serverless

- new paradigm in which the developers do not have to manage servers anymore
- They just deploy code
- Initially: Serverless == FaaS (Function as a Service)
- Now it includes anything that is managed: databases, messaging, storage
- Serverless does not mean there are no servers, it means you just do not manage / provision / see them
- E.g: S3, DynamoDB, Lambda, Fargate

# Lambda

- EC2 Instance - bound to amount of RAM and CPU
- Continuosly running
- Scaling means intervention do add / remove servers
- Lambdas are virtual functions
- Limited by time - short executions
- Run on demand
- Scaling is automated

## Benefits

- Easy pricing: pay per request and compute time
- Free tier of 1,000,000 AWS Lambda invocations and 400,000 GB of compute time
- Integrated with the whole AWS suite of services
- Event Driven - functions get invoked by AWS when needed
- many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per function (up to 10 GB)
- Increasing the RAM wil also improve CPU and network

## Languages

- Node.js
- Java
- C# / Powershell
- Python
- Ruby
- Custom Runtime API (community supported, example Rust or Golang)

- Lambda Container Image - must implement the Lambda Runtime API
- ECS / Fargate is preferred for running arbitrary Docker Images

- E.g.: Serverless Thumbnail creation
- New image in S3 -> triggers AWS Lambda Function -> Creates the thumbnail -> pushes the Thumbnail back to S3

- E.g: Serverless Cron Job
- Cloudwatch Events (EventBridge) -> trigger every 1 hour -> Lambda Function -> perform a task

- Lambda Pricing:
  - first 1,000,000 are free
  - 0,20$ per 1 million requests thereafter
  - pay per duration (in increment of ms):
  - 400,000 GB-seconds of compute time per month is FREE
    - 400,000 seconds if function is 1 GB RAM
    - 3,200,000 seconds if function is 128 MB RAM
  - After that $1,00 for 600,000 GB-seconds
  - it is usually very cheap to run AWS Lambda so it is very popular

# Api Gateway

- Building a serverless API
- Client -> API Gateway -> Proxy Requests -> Lambda -> DynamoDB
- Fully managed service for developers to easily create, publish, mantain, monitor and secure APIs
- SErverless and scalable
- Supports RESTful APIs and Websockets APIs
- Support for security, user authentication, API throttling, API Keys, monitoring

# AWS Batch

- Fully managed batch processing at any scale
- Efficiently run 100,000 of computing batch jobs on AWS
- A "batch" job is a job with a start and an end (opposed to continuos)
- Batch will dynamically launch EC2 instances or Spot Instances
- AWS Batch provisions the right amount of compute / memory
- You submit or schedule batch jobs and AWS Batch does the rest
- Batch jobs are defined as Docker images and run on ECS
- Helpful for cost optimizations and focusing less on the infrastructure

- Simplified example:

  - Process Images from S3
  - S3 -> Trigger -> AWS Batch -> launch the EC2 and Spot Instances -> run on ECS
  - Does the job

- Lambda

  - has a time limit
  - limited runtimes
  - limited temporary disk space
  - serverless

- Batch
  - no time limit
  - any runtime as long as it is packaged as a Docker Image
  - Rely on EBS / instance Store for disk space
  - Relies on EC2 (can be managed by AWS)

# Amazon Lightsail

- Virtual servers, storage, databases, and networking
- Low and predictable pricing
- Simples alternative to using EC2, RDS, ELB, EBS, Route 53...
- Great for People with little cloud experience
- can setup notifications and monitoring of your Lightsail resources
- Use Cases:
  - Simple web applications (templates for LAMP, Nginx, MEAN, nodejs)
  - Websites - templates for wordpress, Magento, Plesk, Joomla
  - Dev / Test Environment
- Has high availability but no auto-scaling, limited AWS integrations
