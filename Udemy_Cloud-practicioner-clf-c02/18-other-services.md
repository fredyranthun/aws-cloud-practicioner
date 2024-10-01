# Other AWS Services

## Amazon WorkSpaces

- Managed Desktop as a Service (DaaS) solution to easily provision Windows or Linux Desktops
- Great to eliminate management of on-premise VDI (virtual desktop infrastructure)
- Fast and Quickly scalable to thousands of users
- Secured data - integrates with KMS
- Pay-as-you-go service with monthly or hourly rates
- decrease latency: provison near the users

## Amazon AppStream 2.0

- Desktop Application Streaming Service
- Deliver to any computer without acquiring, provisioning infrastructure
- **The Application is delivered from within a web browser**
- Workspaces:
  - fully managed VDI and desktop available
  - the users connect to the VDI and open native or WAM applications
  - Workspaces are on-demand or always on
- AppStream 2.0
  - Stream a desktop application to web browser (no need to connect to a VDI)
  - Works with any device (that has a web browser)
  - allows to configure an instance type per application type (CPU, RAM, GPU)

## AWS IoT Core

- Internet of Things - the network of internet-connected devices that are able to collect and transfer data
- AWS IoT Core allows you to easily connect IoT devices to the AWS Cloud
- Serverless, secure and scalable to billions of devices and trillions of messages
- your applications can communicate with your devices even when they aren't connected
- integrates with a lot of AWS services
- Build IoT applications that gather, process, analyze and act on data

## Amazon Elastic Transcoder

- convert media files stored in S3 into media files in the formats required by consumer playback devices (phones etc)
- easy to use
- highly scalable
- cost effective
- fully managed and secure, pay for what you use

## AppSync

- store and sync data across mobile and web apps in real-time
- Makes use of GraphQL
- Client Code can be generated automatically
- integrations with DynamoDB / Lambda
- Real time subscriptions
- Offline data synchronization
- Fine Grained Security
- AWS Amplify can leverage AWS AppSync in the background

## Amplify

- a set of tools and services that helps you develop and deploy scalable full stack web and mobile applications
- Authentication, Storage, API, CI/CD, PubSub, Analytics, AI/ML, Monitoring, Soruce Code From AWS, GitHub, etc

## Application Composer

- visually design and build serverless applications quickly on AWS
- Deploy AWS infrastructure code without needing to be an expert in AWS
- Configure how your resources interact with each other
- Generates Infrastructure as Code
- Ability to import existing CloudFormation / SAM templates to visualize them

## AWS Device Farm

- Fully managed service that tests your web and mobile apps against desktop browsers, real mobile devices and tablets
- Run tests concurrently on multiple devices (speed up execution)
- ability to configure device settings (GPS, language, Wi fi, Bluetooth)

## AWS Backup

- Fully managed service to centrally manage and automate backups across AWS Services
- on-demand and scheduled backups
- supports PITR (Point-in-time Recovery)
- Retention Periods, lifecycle management, Backup Policies,...
- Cross Region Backup
- Cross-Account Backup (using AWS Organizations)

## Disaster Recovery Strategies

- Backup and Restore (cheapest)
- Pilot Light
- Warm Standby
- Multi-Site/Hot-Site (the most expensive)

## AWS Elastic Disaster Recovery (DRS)

- Quickly and easily recover your physical, virtual and cloud based servers into AWS
- Example: protect your most critical databases (including Oracle, MySQL, and SQL Server), enterprise apps (SAP), protect your data from ransomware attacks
- Continuous block-level replication for your servers

## AWS DataSync

- move large amount of data from on-premises to AWS
- Can synchronize to: Amazon S3, Amazon EFS, Amazon FSx for Windows
- Replication tasks can be scheduled hourly, daily, weekly
- The replication tasks are incremental after the first full load

## Cloud Migration Strategies: The 7Rs

- Retire

  - turn off things you don't need
  - helps reducing the surface areas for attacking (more security)
  - Save costs, maybe up to 10 to 20%
  - Focus your attention on resources that must be mantained

- Retain

  - Do nothing for now (it's still a decision to make in a Cloud Migration)
  - Security, data compliance, performance, unresolved dependencies
  - No business value to migrate, mainframe or mid-range and non-x86 Unix apps

- Relocate

  - move apps from on-premises to its Cloud version
  - Move EC2 instances to a different VPC, AWS account or AWS Region
  - Example: transfer servers from VMware Software defined data center to VMware Cloud on AWS

- Rehost "lift and shift"

  - simple migrations by re-hosting on AWS (applications, databases, data)
  - migrate machines (physical, virtual, another Cloud) to AWS Cloud
  - No cloud optimizations being done, applications is migrated as is
  - could save as much as 30% on cost
  - Example: migrate using AWS Application Migration Service

- Replatform "lift and reshape"

  - Example: migrate your database to RDS
  - not changing the core architecture, but leverage some Cloud optimizations
  - save time and money by moving to a fully managed service or Serverless

- Repurchase "drop and shop"

  - Moving to a different product while moving to the cloud
  - often you move to a SaaS platform
  - Expensive in the short term, but quick to deploy
  - Example: CRM to Salesforce.com, CMS to Drupal

- Refactor / Re-architect
  - reimagining how the application is architected using Cloud Native features
  - driven by the need of the business to add features and improve scalability, performance, security and agility
  - Move from a monolithic application to micro-services
  - Example: move an application to Serverless architectures, use AWS S3

## AWS Application Discovery Service

- Plan Migration projects by gathering information about on-premises data centers
- Server utilization data and dependency mapping are important for migrations

- Agentless Discovery
  - VM inventory, configuration, and performance history such as CPU, memory, disk usage
- Agent-based Discovery

  - System configuration, system performance, running processes and details of the network connections between systems

- resulting data can be viewed within AWS Migration Hub

## AWS Application Migration Service

- lift-and-shift (rehost) solution which simplify migration
- Convert your physical, virtual, and cloud-based servers to run natively on AWS
- Corporate data center -> continuous replication -> AWS (Staging and Production instances)
- supports wide range of platforms, Operating Systems and databases
- minimal downtime, reduced costs

## AWS Migration Evaluator

- helps you build a data-driven business case for migration to AWS
- Provides a clear baseline of what your organization is running today
- install agentless collector to conduct broad-based discovery
- take a snapshot of on premises foot-print, server dependencies
- analyze current state, define target state, then develop migration plan

## AWS Migration Hub

- central location to collect servers and applications inventory data for assessment, planning, and tracking to AWS
- Helps accelerate your migrations to AWS, automate lift-and-shift
- AWS Migration Hub Orchestrator - pre-built templates to save time and effort migrating enterprise apps
- supports migrations status updates from Application Migration Service and Database Migration Service

## AWS Fault Injection Simulator (FIS)

- fully managed service for running fault injection experiments on AWS workloads
- Based on Chaos Engineering - stressing an application by creating disruptive events, observing how the system responds, and implementing improvements
- helps you uncover hidden bugs and performance bottlenecks
- supports: EC2, ECS, EKS, RDS
- can use pre-built templates

## AWS Step Function

- build serverless visual workflow to orchestrate your Lambda Functions
- Features: sequence, parallel, conditions, timeouts, error handling,...
- can integrate with EC2, ECS, On-premises servers, API Gateway, SQS Queues, etc.
- Possibility of implementing human approval, feature
- Use cases: order fulfillment, data processing, web applications, any workflow

## AWS Ground Station

- fully managed service that lets you control satellite communications, process data, and scale your satellite operations
- provides a global network of satellite ground stations near AWS regions
- allows you to download satellite data to your AWS VPC within seconds
- send satellite data to S3 or EC2
- use cases: weather forecasting, surface imaging, communications, video broadcast

## AWS Pinpoint

- Scalable 2-way (outbound/inbound) marketing communications service
- supports email, SMS, push, voice, and in-app messaging
- ability segment and personalize messages with the right content to customers
- possibility to receive replies
- scales to billions of messages per day
- use cases: run campaigns by sending marketing, bulk, transactional SMS messages
- versus Amazon SNS or Amazon SES:
  - in SNS and SES you manage each message's audience, content, delivery schedule
  - in Amazon Pinpoint, you create message templates, delivery schedules, highly targeted segments, full campaigns
