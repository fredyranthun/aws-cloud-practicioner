# CloudFormation

- Declarative way of outlining AWS Infrastructure, for any resources (most of them are supported)
- For example:
  - I want a security group
  - I want two EC2 instances using this security group

## Benefits

- Infrastructure as Code
  - no resources are manually created, which is excellent for control
  - Changes to the infrastructure are reviewed through code
- Cost
  - each resource within the stack is tagged with an identifier so you can easily see how much a stack costs you
  - You can estimate the costs of your resources using the cloud formation template
  - Saving strategy: in dev, you could automation deletion of templates at 5 PM and recreated at 8 AM, safely
- Productivity
  - Ability to destroy and recreate a infrastructure on the cloud on the fly
  - Automated generation of Diagram for your template
  - Declarative programming - no need to figure out ordering and orchestration
- Do not reinvent the wheel
  - Leverage existing template on the web
  - Leverage documentation
- Supports almost all resources in AWS
  - You can use "custom resources" for resources that are not supported

## Application Composer

- Visualize the stack graphcally

# AWS Cloud Development Kit (CDK)

- Define your cloud infrastructure using a familiar language: Javascript, Python, Java...
- Code is compiled into a CloudFormation Template
- You can therefore deploy infrastructure and application runtime together
  - great for lambda function
  - great for Docker container in ECS / EKS
- CDK Application -> CDK CLI -> CloudFormation Template -> CloudFormation
- use the features of the programming languages

# Beanstalk

- Typical Architecture:
  - ELB -> EC2 Instances -> RDS and Elasticache (optional)
  - can be reproduced through console or CloudFormation
- Most web apps have the same architecture (ALB + ASG)
- Run the code through different environments
- Elastic Beanstalk is a developer centric view of deploying an application on AWS
- uses all the components we've seen before: EC2, ASG, ELB, RDS...
- We still have control over configuration
- Platform as a Service (PaaS)
- is free, you pay for the underlying instances
- Managed service
  - Instance configuration / OS is handled by Beanstalk
  - deployment strategy is configurable but performed by Elastic Beanstalk
  - capacity provisioning
  - load balancing and auto-scaling
  - application health monitoring and responsiveness
- just the application code is responsibility of the developer
- Three architecture models:
  - Single instance deployment: good for dev
  - LB + ASG: great for production or pre-production web applications
  - ASG only: great for non-web apps in production (workers)
- Support for many platforms: Go, Node, Java, .Net, Ruby, Python, Docker
- Health Monitoring
  - Health agent pushes metrics to CloudWatch
  - Checks for App health, publishes health events
- Uses Cloudformation to create the predefined architecture

# AWS CodeDeploy

- Way to deploy the application automatically
- V1 -> V2 => updates the infra with the new code
- Works with EC2 Instances
- Works with on premises servers
- Hybrid Service
- Servers / Instances must be provisioned and configured ahead of time with the codedeploy agent
- From a single interface

# AWS CodeCommit

- store the application code
- is a competing product from AWS to Github or Gitlab
- Source-control service that hosts Git-based repositories
- make it easy to collaborate with others on code
- the code changes are automatically versioned
- fully managed
- scalable and highly available
- private, secured, integrated with AWS

# AWS CodeBuild

- allows you to build your code in the cloud (compile, run tests)
- Compiles source code, run tests, and produces packages that are ready to be deployed (by CodeDeploy for example)
- E.g: Code is in CodeCommit -> CodeBuild retrieve the code -> build code -> Ready-to-deploy artifact -> CodeDeploy
- Benefits:
  - fully managed, serverless
  - continuosly scalable, highly available
  - secure
  - pay as you go pricing, only pay for the build time

# AWS CodePipeline

- Orchestrate the different steps to have the code automatically pushed to prodution
- Code -> build -> Test -> provision -> Deploy
- Basis for CICD (Continuos Integration and Continuos Delivery)
- Code Pipeline: orchestration Layer
- Code Commit -> CodeBuild -> CodeDeploy -> Elastic Beanstalk
- Fully managed, compatible with CodeCommit, CodeBuild, CodeDeploy, Elastic Beanstalk, CloudFormation, Github, 3rd party services, custom plugins
- Fast delivery and rapid updates

# AWS CodeArtifact

- Software packages depend on each other to be built (code dependecies) and new ones are created
- Storing and retrieving these dependecies is called artifact management
- Codeartifact is a secure, scalable and cost effective artifact management for software development
- works with common dependency management tools such as Maven, Gradle, npm, yarn, twine, pip and NuGet
- Developers and CodeBuild can then retrieve dependencies straight from CodeArtifact
- Similar than npm (for private artifacts, for example)

# AWS CodeStar

- will be discontinued in July 2024
- it will be replaced by CodeCatalyst
- probably will not appear on exam
- Is a unified UI do easily manage software development activities in one place
- quick way to start correctly to set-up CodeCommit, CodePipeline, CodeBuild, CodeDeploy, Elastic Beanstalk, EC2...

# AWS Cloud9

- AWS Cloud9 is a cloud IDE (Integrated Development Environment) for writing, running and debugging code
- use directly in the Web Browser, without any setup necessary
- allows code colaboration at the same time, pair programming...

# AWS SSM - AWS Systems Manager

- Helps you manage your EC2 and on-premises systems at scale
- another Hybrid AWS Service
- Get operational insights about the state of your infrastructure
- Suite of 10+ products
- Most import features are:
  - patching automation for enhanced compliane
  - run commands across an entire fleet of servers
  - Store parameters configuration with the SSM Parameter store
- Works for Linux, Windows, MacOS, Raspberry Pi OS
- SSM Agent must be installed ont the systems we controle
- By default on Amazon Linux AMI and some Ubuntu AMI
- SSM Agent on Instance -> contact directly the SSM
- Thanks to SSM we can run commands, patch and configure our servers

## SSM Session Manager

- Allows you to start a secure shell on your EC2 and on-premises servers
- no SSH Access, bastion hosts, or SSH keys needed
- no port 22 needed (better security)
- EC2 Instance -> SSM Agent -> SSM Session Manager Service -> User
- Can send log data to S3, Cloudwatch...
- IAM in the EC2 instance: role with AmazonSSMManagedInstanceCore permission
- In SSM -> fleet manager -> instance will boot and appear on the Fleet manager Panel
- Session Manager -> start session -> select the instance
- connect the secure shell directly on the browser

## Systems Manager Parameter Store

- Secure storage for configuration and secrets
- API Keys, Password, configurations
- Serverless, scalable, durable, easy SDK
- Control access permissions using IAM
- Version tracking and encryption

# Summary

- CloudFormation: IaaC, repeat across Regions and Accounts
- Beanstalk: PaaS, limited to certain programming languages and Docker, deploy code with a known architecture, eg: ALB + EC2 + RDS
- CodeDeploy: hybrid, deploy and upgrade any application onto servers
- Systems Manager: hybrid, patch, configure and run commands at scale
- CodeCommit: store code in private git repository
- CodeBuild: build and test code in aws
- CodeDeploy: deploy code onto servers
- CodePipeline: orchestration of pipeline (from code to build to deploy)
- CodeArtifact: store software packages / dependencies on AWS
- CodeStar: unified view for allowing developers to CICD and code
- Cloud9: Cloud IDE with collab
- AWS CDK: define cloud infrastructure using a programming language
