# ELB and ASG - Elastic Load Balancing and Auto Scaling Groups

## Scalability and High Availability

- Scalability means your application /system can handle greater loads by adapting
- Two kinds of scalability in the cloud:
  - Vertical Scalability
  - Horizontal Scalability = Elasticity
- Scalability is linked but different to High Availability

## Vertical Scalability

- Means increasing the size of the instance
- E.g: junior operator -> Senior operator, t2.micro -> t2.large
- Vertical scalability is very common for non distributed systems, such as a database
- There is a limit (although very high nowadays)
-

## Horizontal Scalability

- increasing the number of instances / systems for your application
- more employees, more instances
- Implies distributed systems
- very common for web applications / modern applications

## High Availability

- hand in hand with horizontal scaling
- means running your application system in at 2 AZs
- The goal is surviving a data center loss

### Summary

- Vertical Scaling - increase instance size
- Horizontal Scaling - increase the number of instances
  - Auto scaling group
  - Load Balancer
- High Availability - run instances for the same application across multi AZ
  - ASG - multi AZ mode
  - LB in multi AZ mode

## Definitions

- Scalability - ability to accomodate a larger load by making the hardware stronger or by adding nodes
- Elasticity - once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friendly": pay-per-use, match demand, optimize costs
- Agility: new IT resources area only a click away

## Elastic Load Balancer

- Load Balancer are servers that forward internet traffic to multiple servers (EC2 instances) downstream
- Onde LB -> multiple instances
- Expose single point of access (DNS to your application)
- Seamlessly handle failures of downstream instances
- do regular health checks to your instances
- provide SSL termination HTTPS for your websites
- High availability across AZ
- ELB is a manged load balancer
  - AWS guarantees that it will be working
  - takes care of upgrades, maintenance, high availability
  - only a few configuration knobs
- you can setup your own load balancer, but it will be a lot more effort on your end (maintenance, integrations)
- 4 kinds of LB offered by AWS:
  - Application Load Balancer (HTTP/HTTPS only) - layer 7
  - Network Load Balancer (ultra high performance, allows for TCP) - layer 4
  - Gateway Load Balancer - Layer 3
  - Classic Load Balancer - retired in 2023.

### Differences between load balancers

#### ALB

- HTTP / HTTPS / gRPC protocols - layer 7
- HTTP Routing features
- Static DNS (URL)
- Has a target group (can be one or more instances)

#### NLB

- TCP / UDP protocols
- ultra high performance: millions of request per seconds
- Static IP through Elastic IP

#### Gateway Load Balancer

- GENEVE Protocol on IP Packets - Layer 3
- Route traffic to firewalls that you manage on EC2 Instances
- Intrusion detection
- User -> GWLB -> 3rd party Security Virtual Appliances -> back to GWLB -> Application (destination)

## Auto Scaling Group

- the load on your websites can change
- In the cloud, you can create and get rid of servers very quickly
- Scale out - add EC2 Instances to match increase load
- Scale in - remove EC2 Instances to match a decreased load
- Ensure we have a min and a max number of machines running
- Automatically register new instances to a load balancer
- Replace unhealthy instances
- Cost Savings: only run at an optimal capacity (principle of the cloud)
- Auto scaling group in AWS:
  - Actual size / desired capacity: 3
  - Minimum size: 1
  - Maximum size: 6
