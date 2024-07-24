# EC2

## Budget Setup

- Use root account
- Define a budget and alarm for the budget
- Administrator access has no permission to do it.
- IAM and role access to Billing information - activate
- AWS Budgets -> can create alarms with templates.
- E.g.: Zero spend budget -> alarm will show you when you spend more than 1 cent.
- Monthly cost Budget -> get emails when spending gets 85%, forecast gets to 100%.

## EC2 Instances

- Elastic Compute Cloud
- IaaS
- Renting virtual Machines - EC2
- Storing data on virtual drive - EBS
- Distributing loads across machines - ELB
- Scaling the services using an auto-scaling group - ASG
- Fundamental to understand how Cloud works

## EC2 Sizing and configuration options

- OS: Linux, Windows or MacOS
- How much compute power: CPU
- How much RAM
- How much storage space:
  - Network-attached EBS & EFS
  - hardware (EC2 Instance store)
- Network Card: speed, Public IP address
- Firewall rules: security group
- Bootstrap script: EC2 User Data

## EC2 User Data

- A script that runs once at the instance first start
- Automate boot tasks (bootstraping), launching commands when a machine starts
- Install updates, install software, download common files from the internet
- Runs with the root user (sudo)

## EC2 Instances Types

- family.size
- E.g.: t2.micro, t2,xlarge, c5d.4xlarge
- different sizes for the same family
- t2.micro is part of AWS free tier

## Launching a Instance

- Web server launched with EC2 User Data
- Start / stop / terminate instance
- Create Name and Tag (tags are optional)
- Base Image -> OS and predefined image for the instance (architecture)
- Create a key pair to access the instance (.pem for linux, .ppk for Windows previous than 10)
- Network settings
  - Public IP (Auto-assign)
  - Allow SSH traffic from anywhere
  - allow http traffic from internet
- Storage -> default 8 GiB
- Volume will be deleted on termination by default
- Advanced details:
  - User Data: script for being execute on first launch
  - Example:
  ```shell
    yum update -y
    yum install -y httpd
    systemctl start httpd
    systemctl enable httpd
    echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
  ```
- Summary: information about the instance we are launching
- It takes less then one minute to launch the instance
- You can access via the public IP of the instance, which is accessible from internet
- Stop state -> will not charge
- Terminate instance -> will destroy all data related by default

## EC2 Instance Types

- Different types for different use cases
- m5.2xlarge
  - m is the instance class
  - 5 is the generation
  - 2xlarge - size inside the class
- Types of instances:
  - General Purpose - great for a diversity of workloads, as web servers, code repositories,
    balance between compute, memory, networking. Eg: t2.micro
  - Compute Optimized - great for compute intensive tasks (batch processing, media transcoding,
    high performance web servers, high performance computing - HPC, scientific modeling and machine learning,
    dedicated gaming servers) - Eg.: C5, C6
  - Memory optimized - fast performance for large data sets in memory - high performance, relational/non-relational data bases, distributed web scale cache stores, BI, real-time processing of big unstructured data
  - Storage Optimized - storage-intensive tasks require high sequencial read and write access to large data sets
  - and others

## Security Groups

- They are the fundamental of network security in AWS.
- Control how traffic is allowed into or out of our EC2 Instances
- Contain only ALLOW rules
- Security group rules can reference by IP or by security group
- E.g.: security group on EC2 instance, allowing inbound traffic and outbound traffic so we can access the instance from our machine
- Acting as firewall on EC2 instances
- They regulate:
  - Access to ports
  - Authorized IP ranges - IPv4 and IPv6
  - Control of inbound network
  - Control of outbound network
  - Type, Protocol, Port Range, Source, Description
- E.g.: allow my instance to be accessed from my IP on port 22 (ssh). Other computers will be blocked.
- By default, all outbound traffic is allowed (any IP and any port)
- Security groups can be attached to multiple instances
- Instances can have multiple security groups
- Loocked down to a region /VPC combination
- Security groups live outside the EC2 - if traffic is blocked the EC2 instance will not see it.
- Good to mantain separate security group for SSH access.
- Timeout to access is probably security group issue
- Default:
  - all inbound traffic is blocked
  - all outbound traffic is authorized
- Security group can reference/ authorize other Security groups
- So the EC2 instances attached to the authorized security groups will be able allowed to access the initial instance
- This way there is no need to hardcode Instance IPs

## Ports to know

- 22 - SSH - secure shell
- 21 - FTP
- 22 - SFTP - upload files using SSH
- 80 - http - access unsecured websites
- 443 - https - access secure websites
- 3389 - RDP - Remote Desktop Protocol - log into a Windows Instance
