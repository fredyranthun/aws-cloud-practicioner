# Why make a Global Application

- is a application deployed in the the next sprint
- On AWS: This could be Regions or Edge Locations
- Reasons:
- Decreased Latency
  - time it takes for a network packet to reach the server
  - Asia to US
  - Deploy application closer to your users to decrease latency, better experience
- Disaster Recovery
  - if an AWS region goes down
  - you can fail over to another region and your application keeps working
  - A DR plan is important to increase the availability of your application
  - Attack protection: distributed infrastructure is harder to attack

# Global AWS Infrastructure

- Regions: deploying applications and infrastructure
- Availability Zones: made of multiple data centers
- Edge Locations (Points of Presence): for content develivery as close as possible to users
- about 33 regions (currently)
- 105 AZs and +600 PoP
- Cloudfront uses PoP
- AWS has Networks as well, as cables under the water to link US and Europe, for example

# Global Applications in AWS

- DNS: Route 53
  - great to route users to the closest deployment with least latency
  - great for disaster recovery strategies
- Global CDN (Content Delivery Network): Cloudfront
  - replicate part of your application to AWS Edge Locations - decrease latency
  - cache common requests - improved user experience and decreased latency
- S3 Transfer Acceleration
  - accelerate global uploads and downloads into S3
- AWS Global Accelerator
  - improve global application availability and performance using the AWS Global netowork

# Amazon Route 53

- Domain Name System (DNS)
- DNS is a collection of rules and records which helps clients understand how to reach a server through URLs
- In AWS the most common records are:
  - www.google.com -> 12.34.56.78 -> A record (IPv4)
  - www.google.com -> 2001:0db8:85a3:0000:0000: ... -> AAAA IPv6
  - search.google.com -> www.google.com -> CNAME:hostname to hostname
  - example.com -> AWS resource == ALIAS (ex: ELB, Cloudfront, S3, RDS...)

## Diagram for A Record

- Web Browser to access a application server (IP 32.45.67.85)
- Route 53 -> create A Record.
- Browser -> DNS Request "myapp.mydomain.com" -> Route 53 replies back with IP 32.45.67.85 (A record: hostname to IP)
- Browser than makes an HTTP Request to IP 32.45.67.85, the application server sends the HTTP Response

## Routing Policies

- Need to know them at a high-level for the Cloud Practicioner Exam
- **Simple Routing Policy**
  - No health checks
- **Weighted Routing Policy**
  - Assign weights to our EC2 Instances, and Route 53 will redirect based on the weights
  - Type of load balancing
- **Latency Routing Policy**
  - look where the user is located and redirect to the nearest server
  - minimize the latency
- **Failover Routing Policy**

  - Health check on primary, redirect to the failover

- You can register domain in Route 53
- You can link the domain to different EC2 instances, for example, and use the latency policy
- Instances in different regions will be linked to the same domain

# AWS CloudFront

- CDN - Content Delivery Network
- Improves read performance, content is cached in the edge
- Improves Users Experience
- 216 PoP globally (edge locations)
- DDoS protection (because worldwide), integration with Shield, AWS WAF
- User -> PoP -> searchs content from S3 -> Caches -> Next user will have the content cached

## Origins

- S3 bucket

  - for distributing files and caching them at the edge
  - Enhanced security with CloudFront Origin Access Control (OAC)
  - OAC is replacing Origin Access Identity (OAI)
  - Cloudfront can be used as an ingress (to upload files to S3)

- Custom Origin (HTTP)

  - Application Load Balancer
  - EC2 Instance
  - S3 Webisete
  - Any http backend you want

- Client -> CloudFront (CDN) -> If Cache -> returns to Client -> Or Forward Request to Origin
- Local Cache is updated with the content
- E.g: Edge Los Angeles -> get from S3 Bucket (origin)
- Content is distributed all around the world in Edge Locations or Points of Presence

- Difference CloudFront and S3 Cross Region Replication
- CloudFront

  - Global Edge Network
  - Files are cached for a TTL (maybe a day)
  - Great for static content that must be available everywhere

- S3 Cross Region Replication
  - Setup for each region you want the replication to happen
  - Files are updated in near real-time
  - Read only
  - great for dynamic content that needs to be available at low-latency in few regions

# S3 Transfer Acceleration

- File in USA -> Edge Location -> S3 Bucket Australia
- Increase transfer speed by transfering file to an AWS edge Location which will forward the data to the S3 bucket in the target region (uses internal AWS private network)

# AWS Global Accelerator

- User -> Public Internet -> Closest Edge Location -> Private AWS -> Public ALB in us-east-1 (example)
- Improve global application availability and performance using the AWS global network
- Levarage AWS internal network to optimize the route to your application (60% improvement)
- 2 Anycast IP -> are created for your application and traffic is sent through Edge Locations
- Edge Location will send the traffic to your application

## Difference between CloudFront and AWS Global Accelerator

- They both use AWS Global network nad its Edge Locations around the world
- Both services integrate with AWS Shield for DDoS protection
- CloudFront - CDN
  - improves performance for cacheable content (such as images and videos)
  - Content is server at the edge
- Global Accelerator
  - no caching, proxing packets at the edge to applications running in one or more AWS Regions
  - Improves performance for a wide range of applications over TCP and UDP
  - Good for HTTP use cases that require static IP adresses
  - Good for HTTP use cases that require deterministic, fast regional failover

# AWS Outposts

- Hybrid Cloud: keep an on-premises infrastructure alongside a cloud infrastructure
- Therefore, two ways of dealing with IT systems:
  - one for the AWS Cloud (AWS Console, CLI and APIs)
  - One for their on-premises infrastructure
- AWS Outposts are "server racks" that offers the same AWS infrastructure, services, APIs and tools to build your own applications on-premises just as in the cloud
- AWS will setup and manage "Outposts Racks" within your on-premises infrastructure and you can start leveraging AWS services on-premises
- You are responsible for the Outposts Rack

## Benefits

- Low-latency to on-premises- systems
- Local data processing
- Data residency
- Easier migration from on-premises to the cloud
- fully managed service
- Some services working on Outposts: EC2, EBS, S3, EKS, ECS, RDS, EMR

# AWS Wavelength

- Bring AWS services to the edge of 5G Network
- Are infrastructure deployments embedded within the telecommunications providers datacenter at the edge of 5G network
- Traffic does not leave Communication Service Providers Network
- High-bandwith and secure connection to the parent AWS Region
- No additional charges or service agreements

# AWS Local Zones

- Places AWS compute, storage, database, and other AWS services closer to end users to run **latency-sensitive applications**
- extend your VPC to more locations - "Extensios of an AWS Region"
- Compatible with EC2, RDS, ECS, EBS, ElastiCache, Direct Connect
- Example:
  - AWS Region: us-east-1
  - 6 AZs
  - extend your VPC to a local zone, in Boston (us-east-1-bos-1a) or Chicago, for example
- In some regions you have AZ, and Local Zones that are disabled by default

# Global Applications Architecture

## Single Region, Single AZ

- Not high availability
- high global latency
- low difficulty

## Single Region, Multi AZ

- High Availability
- high global latency
- slightly more difficult

## Multi Region, Active-Passive

- Multiple regions
- in one region users can Read and write
- in other region, users can only read
- Low reads' latency
- High writes' latency
- more difficult

## Multi Region, Active-Active

- Users can read and write from many regions
- Low reads' and writes' latency
- higher difficult
- E.g.: Dynamo DB multi region

# Summary

- Global DNS: Route 53
  - route user to the closest deployment with least latency
  - great for disaster recovery strategies
- Global CDN: CloudFront
  - Replicate part of your application data do AWS Edge Locations
  - cache common requests
- S3 Transfer Acceleration
  - Accelerate global uploads and downloads into AWS S3
- AWS Global Accelerator
  - improve global application availability and performance using the AWS Global network
- AWS outposts
  - deploy outposts Racks in our own datacenter to extend AWS services
- AWS Wavelength
  - brings AWS to the edge of 5G networks
  - ultra-low latency applications
- AWS Local Zones
  - Bring AWS resources (compute, database, storage) closer to your users
  - good for latency sensitive applications
