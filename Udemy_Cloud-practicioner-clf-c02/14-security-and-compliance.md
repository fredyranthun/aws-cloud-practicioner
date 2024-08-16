# AWS Shared Responsibility Model

## AWS Responsibility

- Security of the cloud
- protecting infrastructure (hardware, software, facilities and networking) that runs all the services
- Managed services like S3, DynamoDB, RDS

## Customer Responsibility

- Security in the Cloud
- EC2 Instance, customer is responsible for management of the Guest OS, firewall and network configuration, IAM
- Encrypting application data

## Shared

- Patch Management, Configuration Management, Awareness and training
- E.g: in RDS, AWS does the Patch management for you, in EC2 you are responsible
- You must train your employees correctly

### RDS

#### AWS

- manage the underlying EC2 Instance, disable ssh access
- automated DB patching
- audit the underlying instance and disks and guarantee it functions

#### You

- check if the ports / IP / security groups inbound rules in DB2s SG
- In-database user creation and permissions
- Creating a database with or without public access
- ensure parameter groups or DB is configured to only allow SSL connections
- Database Encryption setting

### S3

#### AWS

- guarantee you get unlimited storage
- Guarantee you get encryption
- ensure separation of the data between different customers
- ensure AWS employees can't access your data

#### You

- Bucket configuration
- Bucket policy / public setting
- IAM user and roles
- enabling encryption

# DDoS Attack

- distributed denial-of-service attack
- multiple servers launching bots doing many requests
- normal users will not me able to connect (Service denied)
- AWS Shield Standard: protect against DDPS attack for your website and applications, for all customers at no additional costs
- AWS Shiel Advanced: 24/7 premium DDoS protection
- AWS WAF: Filter specific requests based on rules
- Cloudfront and Route 53:
  - availability protection using global edge network
  - Combined with AWS Shield, provides attack mitigation at the edge
- Be ready to scale: leverage AWS Auto Scaling

## Sample reference Architecture for DDoS Protection

- Users -> Route 53 (protected by shield) -> Cloudfront distribution (Cache on the edge) - is protected by shield and can be using WAF -> Load Balance on public subnet -> EC2 instances on auto scaling group, scale to higher demands in private subnet

# AWS Shield

## AWS Shield Standard

- free service activated for every AWS customer
- provides protection from attacks such as SYN/UDP Floods, Reflection Attacks and other layer 3 / layer 4 attacks

## AWS Shield Advanced

- optional DDoS mitigation service ($3,000 per month per organization)
- protection against more sophisticated attack on EC2, ELB, Cloudfront, Global Accelerator, and Route 53
- 24/7 access to AWS DDoS response team (DRP)
- Protect against higher fees during spikes due to DDoS

# AWS WAF

- Web Application Firewall
- protects your web applications from common web exploits (Layer 7)
- Layer 7 is HTTP
- Deploy on Application Load Balancer, API Gateway, CloudFront
- Rules can include IP Addresses, HTTP headers, HTTP Body, or URI strings
- protects from common attack - SQL injections and Cross Site Scripting (XSS)
- size constraints, geo-match (block countries)
- rate-based rules - count occurence of events - for DDoS protection

# AWS Network Firewall

- Protect your entire VPC
- From Layer 3 to Layer 7 protection
- Any direction, you can inspect:
  - VPC to VPC traffic
  - Outbound to internet
  - Inbound from internet
  - To / from Direct Connect and Site-to-Site VPN

# AWS Firewall Manager

- Manage security rules in all accounts of an AWS Organization
- Sercurity policy: common set of security rules
  - VPC security groups for EC2, Application Load Balancer, etc
  - WAF Rules
  - AWS Shield Advanced
  - AWS Networkk Firewall
- Rules are applied to new resources as they are created (good for compliance) across all and future accounts in your Organization

# Penetration Testing

- Attack your infra to test your security
- AWS are welcome to carry out security assessments or penetration test against their AWS infra without prior approval for 8 services:
  - EC2 instances, NAT Gateways, and ELB
  - RDS
  - CloudFront
  - Aurora
  - API Gateways
  - AWS Lambda and Lambda Edge functions
  - Lightsail resources
  - Elastic Beanstalk environments
- List can increase over time
- Prohibited Activities:
  - DNS zone walking via Amazon Route 53 Hosted Zones
  - Denial of service (DoS), DDoS, Simulated DoS, Dimulated DDoS
  - Port Flooding
  - Protocol flooding
  - Request flooding
- For other simulated events, contact aws-security-simulated-events@amazon.com

# Encryption

- Data at rest: on a hard disk, RDS instance, in S3 Glacier Depp Archive...
- In transit (in motion): data being moved from one location to another
  - transfer from on-premises to AWS, EC2 to DynamoDb...
  - means data transfered on the network
- Data must be encrypted in both states to protect it.
- we leverage **encryption keys**

## AWS KMS - Key Management SErvice

- AWS manages the encryption keys for us
- Encryption opt-in:

  - EBS Volumes encrypt volumes
  - S3 buckets: server side encryption of objects
  - Redshift database
  - RDS database
  - EFS Drives

- Encryption automatically enabled:
  - CloudTrail Logs
  - S3 Glacier
  - Storage Gateway

## AWS CloudHSM

- AWS provisions encryption hardware
- Dedicated hardware (HSM = Hardware Security Module)
- You manage your own encryption keys entirely (not AWS)
- HSM device is tamper resistant, FIPS 140-2 Level 3 compliance
- AWS manages the hardware -> you manage the keys

## Types of KMS Keys

- Customer managed key
  - create, manage and used by the customer, can enable or disable
  - possibility of rotation policy
  - possibility to bring-your-own-key
- AWS Managed Key
  - created, managed and used on the customer's behalf by AWS
  - used by AWS Services
- AWS Owner Key
  - collection of CMKs that an AWS service owns and manages to use in multiple accounts
  - AWS can use those to protect resources in your account (but you can't view the keys)
- CloudHSM Keys (custom keystore)
  - Keys generate from your own CloudHSM hardware device
  - Cryptographic operations are performe within the CloudHSM Cluster

# AWS Certificate Manager (ACM)

- Let's you easily provision, manage, and deploy SSL/TLS Certificates
- Used to provide in-flight encryption for websites (HTTPS)
- Supports both public and private TLS certificates
- AWS Certificate Manager -> provision and mantain TLS certs -> Application Load Balancer -> HTTP -> ASG
- Free of charge for public TLS certificates
- Automatic TLS certificate renewal
- Integrations with (load TLS certificates on):
  - Elastic Load Balancer
  - Cloudfront Distributions
  - APIs on API Gateway

# AWS Secrets Manager

- newer service, meant for storing secrets
- capability to force rotation of secrets every X days
- Automate generation of secrets on rotation (uses Lambda)
- Integration with RDS (MySQL, PostgreSQL, Aurora)
- Secrets are encrypted using KMS
- Mostly meant for RDS integration

# AWS Artifact

- Portal that provides customers with on-demand access to AWS compliance documentation and AWS agreements
- Artifact Reports: allows you to download AWS security and compliance documents from third-party auditors like AWS Iso certifications, Payment Card Industry, and System and Organization Control (SOC) reports
- Artifact Agreements: allows you to review, accept, and track the status of AWS agreements such as the Business Associate Addendum (BAA) or the Health Insurance Portability and Accountability Act (HIPAA) for an individual account or in your organization
- can be used to support internal audit or compliance

# Amazon GuardDuty

- Intelligent Threat discovery to protect your AWS account
- uses Machine Learning algorithms, anomaly detection, 3rd party data
- one click enable (30 days trial), no need to install software
- Input data includes:
  - CloudTrail Event Logs
  - VPC Flow Logs
  - DNS Logs
  - Optional Features (S3 logs, Lambda network activity, EBS Volumes, RDS and Aurora Login Activity)
- Can setup EventBridge rules to be notified in case of findings
- EventBridges rules can target AWS Lambda or SNS
- Can protect against CryptoCurrency attacks (has a dedicated "finding" for it)
- Input Info -> Guard Duty -> Event Bridge -> SNS or Lambda

# Amazon Inspector

- Run automated security assessments
- For EC2 Instances
  - Leveraging the AWS System Manager (SSM) agent
  - Analyze against unintended network accessibility
  - Analyze running OS against known vulnerabilities
- Container Images push to Amazon ECR
  - Assessment of Container Images as they are pushed
- Lambda Functions

  - Identifies software vulnerabilities in function code and package dependencies
  - assessment of functions as they are deployed

- Reporting and integration with AWS Security Hub
- Send findings to Amazon EventBridge
- only for EC2 Instanes, Container Images, Lambda functions
- Continuos scanning of the infrastructure, only when needed
- Package vulnerabilities (EC2, ECR and lambda) - database of CVE
- Network Reachbility - EC2
- A risk score is associated with all vulnerabilities for prioritization

# AWS Config

- Helps with auditing and recording compliance of your AWS resources
- Helps record configuration and changes over time
- Possibility of storing the configuration data into S3 (Analyzed by Athena)
- Questions that can be solve by AWS Config
  - Is there unrestricted access to my security groups?
  - do my buckets have any public access?
  - How has my ALB configuration changed over time?
- You can receive alerts (SNS Notifications) for any changes
- AWS Config is a per-region service
- Can be aggregated across regions and accounts

## AWS Config Resource

- View compliance of a resource over time
- view configuration of a resource over time
- view cloudtrail API calls if enabled

# Amazon Macie

- Fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS
- Macie helps identify and alert you to sensitive data such as personally identifiable information (PII)
- S3 Buckets -> Macie Analyze (discover PII) -> notify Amazon EventBridge -> integrations

# AWS Security Hub

- Central security tool to manage security across several AWS accounts and automate security checks
- Integrates dashboards showing current security and compliance status to quickly take actions
- Automatically aggregates alerts in predefined or personal findings formats from various AWS services and AWS partner tools
  - Config
  - GuardDuty
  - Inspector
  - Macie
  - IAM access Analyzer
  - AWS Systems Manager
  - AWS Firewall Manager
  - AWS Health
  - AWS Partner Network Solutions

# Amazon Detective

- Guard Duty, Macie, Security Hub are used to identify potential security issues, or findings
- sometimes security findings require deeper analysis to isolate the root cause and take action - it is a complex process
- Amazon Detectie analyzes, investigates, and quickly identifies the root cause of security issues or suspicious activities (using ML and graphs)
- Automatically collects and processes events from VPC flow logs, CloudTrails, GuardDuty and create a unified view
- Produces visualizations with details and context to get to the root cause

# AWS Abuse

- Report suspected AWS resources used for abusive or illegal purposes
- Abusive and prohibited behaviors are:
  - Spam: receiving undesired email from AWS-owned IP address, websites and forums spammed by AWS resources
  - Port scanning: sending packets to your ports to discover the unsecured ones
  - DoS DDoS attacks
  - Intrusion attempts - logging in on your resources
  - Hosting objectionable or copyrighted content: distributing illegal or copyrighted content without consent
  - Distributing Malware - AWS resources distributing softwares to harm computers or machines
- Contact the AWS Abuse Team: AWS Abuse Form or abuse@amazonaws.com

# Root User Privileges

- Account Owner (Created when account is created)
- has complete access to all AWS services and resources
- Lock away your AWS account root usr access keys
- Do not use Root user for everyday tasks
- Actions that can be performed only by the root user:
  - **Change account settings** (Account name, email address, root user password, root user access keys)
  - View certain tax invoices
  - **Close your AWS Account**
  - Restore IAM user Permissions
  - **Change or cancel you AWS Support Plan**
  - **Register as a seller in the Reserved Instance MarketPlace**
  - Configure S3 Bucket to enable MFA
  - Edit or delete an Amazon S3 bucket policy that includes an invalid VPC ID or VPC Endpoint ID
  - Sign up for GovCloud

## IAM Access Analyzer

- Find out which resources are shared externally
  - S3 Buckets
  - IAM Roles
  - KMS Keys
  - Lambda Functions and Layers
  - SQS Queues
  - Secrets Manager Secrets
- Define Zone of Trust = AWS account or AWS Organization
- Access outside zone of trust -> findings
- E.g: S3 Buckets public

# Summary

- Shared Responsibility on AWS
- Shield: Automatic DDoS Protection + 24/7 for advanced
- WAF: Firewall to filter incoming request based on rules
- KMS: Encryption Keys managed by AWS
- CloudHSM: Hardware Encryption, we manage encryption keys
- AWS Certificate manager: provision, manage and deploy SSL/TLS Certificates
- Artifact: Get access to compliance reports such as PCI, ISO...
- GuardDuty: fin malicious behavior with VPC, DNS and CloudTrail logs
- Inspector: find software vulnerabilities in EC2, ECR and Lambda functions
- Network Firewall: protect your VPC against network attacks
- Config: track config changes and compliance againts rules
- Macie: Find sensitive data (ex: PII data) in Amazon S3 Buckets
- CloudTrail: Track API calls made by users within account
- AWS Security Hub: gather security findings from multiple AWS accounts
- Amazon Detective: find the root cause of security issues or suspicious activities
- AWS Abuse: report AWS resources used for abusive or illegal purposes
- Root use priviledges:
  - Change account settings
  - Close your AWS account
  - Change or cancel your AWS Support Plan
  - Register as a seller in the Reserved Instance Marketplace
- IAM Access Analyzer: identify which resources are shared externally
- Firewall Manager: manage security rules across an Organization (WAF, Shield...)
