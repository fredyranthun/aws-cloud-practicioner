# Cloud Practiticione - Udemy Notes

## Create a personal account in AWS

- Support plan: Basic (free)
- it takes a credit card
- you create the root account (email and password)

## Cloud and cloud computing

- Websites: server - client (web browser) - network
- Clients and servers have IP addresses
- Similar to post mail
- Server is computer with CPU RAM (generally a powerful machine)
- Storage (can be in the form of a database)
- Network: routers, switch, DNS server
- Router: forward data packets.
- Computer -> router -> switch -> other computers, servers.

### Cloud Computing

Is the on-demand delivery of compute power, database storage, applications and other IT resources.
(pay as you go pricing)
Is a simple way to access servers, storage, databases and a set of application services.

AWS owns and mantains the network-connected hardware required for these application services.

### Deployment Models of the Cloud

#### Private cloud

- Cloud services used by a single organization, not exposed to the public
- Complete control
- Security fo sensitive applications
- Meet specific business needs

#### Public Cloud

- Cloud resources owned and operated by a third-party cloud service provider delivered over the internet.

#### Hybrid Cloud

- keep some servers on premise and extend some capabilities on cloud
- controle over sensitive assets in your private infrastructure
- flexibility and cost effectiveness of the cloud

### Five characteristics of cloud computing

- on-demand seld service
- broad network access
- multi-tenancy and resource pooling: multiple customers share the same infrastructure and applications with security and privacy
- rapid elasticity and scalability
- quickly and easily scale based on demand
- measured service

### Six advantages of cloud computing

- trade capital expense (CAPEX) for operational expense (OPEX)
- Benefit from massive economies of scale
- Stop guessing capacity
- increase speed and agility
- stop spending money running and maintaining data centers
- go global in minutes

### Problems solved

- flexibility
- cost-effectiveness
- scalability
- elasticity
- high-availability
- agility

### Types of cloud computing

-Infrastructure as a Service (IaaS): provide building blocks for cloud IT, networking, computers, data storage, highest level of flexibility (parallel with traditional on-premises IT) - EC2

- Platform as a Service (PaaS): removes the need to manage the underlying infrastructure - focus on deployment and management - Elastic Beanstalk
- Software as a Service (SaaS): completed product that is run and managed by service provider - E.g: Rekognition, Dropbox, Zoom.

### Pricing

- Compute - pay for compute time
- Storage - pay for stored data in the cloud
- Networking - data transfer OUT of the cloud

### AWS Infrastructure

- Global infrastructure
- AWS Regions all around the world
- A region is a clusted of data centers.
- most services are region-scoped.

#### How to choose a region

- compliance - data governance and legal requirements
- proximity to customers: reduced latency
- available services within a region
- pricing

### Availability Zones

- each region has many AZ (usually 3, max is 6)
- Each AZ is one or more discrete data centers with redundant power, network and connectivity.
- AZs in a region are connected with high bandwidth, ultra-low latency networking.

### AWS Points of presence (Edge Locations)

- 400+ points of presences in 90+ cities and 40+ countries
- Content is delivered to end users with lower latency
