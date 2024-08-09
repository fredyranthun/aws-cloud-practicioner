# VPC

## IP Addresses in AWS

### IPv4 - Internet Protocol Version 4 (4.3 Billion Addresses)

- Public IPv4 - can be used on Internet
- EC2 Instance gets a new public IPv4 address every time you stop then start it
- Private IPv4 - ca be used on private networks (LAN) sush as internal AWS networking (e.g.: 192.168.1.1)
- Private IPv4 is fixed for EC2 Instances even if you start/stop them

### Elastic IP

- allows you to attach a fixed IPv4 address to EC2 Instance

- All IPv4 on AWS will be charged 0.005$ per hour (including EIP)

### IPv6 Internet protocol version 6

- Every IP Address is public in AWS (no private range)
- They are free in AWS

## VPC

- Virtual Private Cloud: private network to deploy your resources (regional resource) - specific region
- Subnets allows you to partition your network inside your VPC (AZ resource)
- E.g: AZ A -> Public Subnet -> access to the internet -> internet can reach our public subnet
- Private Subnet -> can not be reached by internet
- To define access to the internet and between subnets, we define Route Tables
- AWS Cloud -> Region -> VPC -> VPC CIDR Range: 10.0.0.0/16
- VPC can be multi AZ
- AZ1 -> Public Subnet and a Private Subnet
- AZ2 -> Public Subnet and a Private Subnet

## Internet Gateways and NAT Gateways

- **Internet Gateways** helps our VPC instances connect with the internet
- VPC will have a Internet Gateway, and the public subnet have a route to the internet Gateway
- **NAT Gateways** (AWS-managed) and NAT Instances allow your instances in your **Private Subnets** to access the internet while remaining private
- Private Subnet -> Public Subnet -> NAT -> IGW -> Internet

## Network ACL and Security Groups

### NACL

- Access Control List
- Firewall which controls traffic from and to subnet
- can have ALLOW and DENY rules
- are attached at the Subnet Level
- Rules only include IP Addresses
- Stateless

### Security Groups

- A firewall which controls traffic from and to an EC2 instance
- Can have only ALLOW rules
- Rules include IP and other security groups
- Stateful

- Default Network ACL is associated with our Subnets automatically at creation

## VPC Flow Logs

- Capture Information about IP traffic goint into your interface
  - VPC Flow Logs
  - Subnet Flow Logs
  - Elastic Network Interface Flow Logs
- Helps to monitor and troubleshoot connectivity issues. Example:
  - Subnets to internet
  - Subnets to subnets
  - Internet to subnets
- Captures network information from AWS managed interfaces too: Elastic Load Balancers, Elasticache, RDS, Aurora
- VPC Flow Logs can go to S3, CloudWatch Logs and Kinesis Data Firehose

## VPC Peering

- Connect to VPCs, privately using AWS network
- VPC A <-> VPC B (VPC Peering)
- Make them behave as if they were in the same network
- Must not overlapping CIDR
- is not transitive, must be estabilished for each VPC that need to communicate with one another

## VPC Endpoints

- Allow you to connect to AWS Services using a private network instead of the public www network
- Gives you better security and lower latency to access AWS Services
- VPC Endpoint Gateway: S3 and DynamoDB
- VPC Endpoint Interface: the rest of the services
- E.g.: EC2 Instance in a private subnet -> VPC Endpoint Interface -> Cloudwatch

## AWS PrivateLink (VPC Endpoint Service)

- Most secure & scalable way to expose a service to 1000s of VPCs
- VPC Peering is not secure or scale very well
- Does not require internet gateway, NAT, Route Tables
- 3rd Part VPC with Application Service -> My VPC with Customer Application
- Requires a Network load balancer - NLB (Service VPC) and Elastic Network Interface - ENI (Customer VPC)

## Site to Site VPN & Direct Connect

### Site to Site VPN

- Connect an on-premises VPN to AWS
- The connection is automatically encrypted
- Goes over the public internet
- On-premises DC -> public internet -> Site-to-Site VPN (encrypted) -> Public internet -> VPC
- security concerns, limited bandwidth
- Corporate Data Center -> Customer Gateway -> **Site-to-Site VPN** -> Virtual Private Gateway -> Private Subnet

### Direct Connect (DX)

- Establish a physical connection between on premises and AWS
- The connection is private, secure and fast
- Goes over a private network
- Takes at least a month to establish
- More expensive

## AWS Client VPN

- Connect your private PC to your Private VPC
- Connect from your computer using OpenVPN to your private network in AWS and on-premises
- Connect EC2 Instances over a private IP - as if you were in the private VPC network
- Goes over public Internet
- Computer with AWS Client VPN (OpenVPN) <-> Internet <-> AWS VPC

## Transit Gateway

- For having transitivie peering between thousands of VPC ad on-premises, hub-and-spoke (star) connection
- Don't need to peer all VPCs
- One single gateway to provide this functionality
- Works with direct connect gateway, VPN Connections

## Summary

- VPC: Virtual Private Cloud
- Subnets: Tied to AZ, network partition of VPC
- Internet Gateway: at the VPC level, provide Internet Access
- NAT Gateway/Instances: give internet access to private subnets
- NACL: Stateless, subnet rules for inbound and outbound
- SEcurity Groups: Stateful, operate at EC2 instance level ENI
- VPC Peering: connect two VPC with non overlaping IP ranges, nontransitive
- Elastic IP - fixed public IPv4
- VPC Endpoints: provide private access to AWS within VPC
- PrivateLink: Privately connect to a service in a 3rd party VPC
- VPC FLow logs: network traffic logs
- Site to Site VPN: VPN over public internet between on-premises DC and AWS
- Client VPN: OpenVPN connection from your computer into your VPC
- Direct Connect: direct private connection to AWS
- Transit Gateway: Connect thousands of VPC and on-premises networks together
