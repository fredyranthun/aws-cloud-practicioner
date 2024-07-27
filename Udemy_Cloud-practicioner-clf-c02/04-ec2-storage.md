# EC2 Storage

## EBS Volumes

- Elastic Block Store Volume is a network drive you attach to your instance while they run
- Allows instances to persist data, even after termination
- Can only be mounted to one instance at a time (CCP level)
- Bound to specific AZ
- as network USB sticks
- 30 GB of free tier EBS Volumes - General Purpose (SSD) or Magnetic per month
- It is a network drive, a little bit o latency
- can be detached from one instance and attached to another
- To move across AZ, you need to snapshot it
- Have to provision capacity in advance (size in GB and IOPs)
- you can improve capacity over time
- billed for the provisioned capacity
- We can attach two EBS volumes to a single instance
- They do not need to be attached all the time
- Delete on termination attribute - by default it is true for root volume and not for other attached EBS Volume
- You can change the default behavior in the console
- EBS Multi Attach is not in the scope of the exam

## EBS Snapshot

- Make a backup of EBS Volume at a point in time
- Not necessary to detach to do snapshot, but recommended
- Can copy snapshots across AZ or Region
- Snaphot from us-east-1a -> can be used to restore a EBS Volume in other region or AZ
- EBS Snapshot Features
  - EBS Snapshot Archive - 75% cheaper, but it takes 24 to 72 hours to restore the archive
  - Recycle bin - retain deleted snapshots, specify retention from 1 day to 1 year

## AMI - Amazon Machine Image

- AMI are a customization of an EC2 instance
- you can add software, configuration, operating system, monitoring
- faster boot, configuration time, because all your software is pre-packaged
- for specific region (can be copied across regions)
- You can launch instances from:
  - public AMI (AWS provided)
  - your own AMI - you make and maintain them yourself
  - AWS Marketplace AMI - someone else made and potentially sells

### AMI process

- Start EC2 instance and customize it
- Stop the instance (for data integrity)
- Build an AMI - create EBS Snapshots behind the scene
- Launch instances from other AMIs
- the user data script will already be set in the new instances

## EC2 Image Builder

- Used to automate the creation of Virtual Machines or container images
- Automate the creation mantain validate and test EC2 AMIs
- EC2 Image Builder -> create -> Builder EC2 Instance -> New AMI -> Test EC2 Instance (test suite is run) -> AMI is distributed (can be multiple regions)
- Can be run on a schedule (weekly, whenever packages are updated)
- Free service - only pay for the underlying resources

## EC2 Instance Store

- If you need high-performance hardware disk, use EC2 Instance Store
- Hardrive attached to the server
- Better I/O performance
- EC2 Instance Store lose their storage if they are stopped
- Good for buffer, cache, scratch data, temporary content
- risk of data loss if hardware fails
- backups and replication are your responsability

## EFS

- Elastic File System
- Managed NFS (network file system)
- can be mounted in 100s of EC2
- Works with Linux instances in multi AZ
- Highly Available, scalable, expensive, pay per use, no capacity planning
- Differences between EBS x EFS
  - EBS available in only one AZ, EFS in multi AZ
  - EFS can be mounted in multiple instances
- EFS-IA - infrequent access - cost-optimized
- automatically moved to EFS-IA if enabled, based on the lifecycle policy
- E.g.: move files that are not accessed for 60 days to EFS-IA

## Shared Responsibility for EC2 Storage

- AWS responsible for:
  - Infrastructure
  - Replications for data for EBS volumes and EFS drives
  - Replacing faulty hardware
  - ensuring employees can not access data
- You is responsible for:
  - setting backup and snapshot procedures
  - setting up data encryption
  - Responsibility for any data on the drives
  - understand the risk of Using EC2 Instance Store

## Amazon FSX

- Fully managed service

### FSX for Windows File Server

- fully managed, highly reliable and scalable Windows Native shared file system
- Supports SMB protocol and Windows NTFS
- Integrated with Microsoft Active Directory

### FSX for Lustre

- fully managed, high performance, scalable file storage fro High Performance Computing (HPC)
- Linux + Cluster
- Machine Learning, Analytics, Video Processing, Finantial modeling,
- Scales up to 100 GB, millions of IOPS, sub-ms latencies

## Summary

- EBS Volumes - network drives, on EC2 instance at a time, one AZ
- AMI - create ready to use EC2 instances
- EC2 Image Builder - automatically build, test, distribute AMIs
- EC2 Instance Store - high performance hardware, lost if instance is stopped or terminated
- EFS - network file system, multi AZ, multi Instances
- EFS-IA - cost effective for EFS
- FSx for Windows, FSx for Lustre
