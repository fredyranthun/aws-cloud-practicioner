# Amazon CloudWatch Metrics

- CloudWatch provides metrics for every service in AWS
- Variable to monitor
- Metrics have timestamps
- can create a dashboard for monitoring metrics
- Example: Cloudwatch Billing Metric

## Important Metrics

- EC2 Instances: CPU Utilization, Status Checks, Network (not RAM)
  - default metrics every 5 minutes
  - option for detailed monitoring ($$$): metrics every 1 minute
- EBS volumes: disk read/writes
- S3 buckets: bucket size bytes, number of objects, all requests
- Billing: total estimated charge
- Service limits: how much you have been using a service API
- Custom metrics

# Cloudwatch Alarms

- Alarms are used to trigger notifications for any metric
- Alarms actions:
  - Auto Scaling: increase or decrease EC2 instances desired count
  - EC2 Actions: stop, terminate, reboot or recover an EC2 instance
  - SNS notifications: send a notification into an SNS topic
- Various options (sampling, %, min, max)
- Can choose the period on which to evaluate an alarm
- Example: create a billing alarm on the Cloudwatch Billing metric
- Alarm State: OK, INSUFFIENTE_DATA, ALARM

# CloudWatch Logs

- can collect log from:

  - Elastic beanstalk
  - Lambda
  - ECS
  - CloudTrail (based on filter)
  - Cloudwatch log agents: on EC2 machines or on-premises servers
  - Route53: Log DNS queries

- Enables real-time monitoring of logs
- Adjustable CloudWatch Logs retention

## CloudWatch Logs for EC2

- By default no logs from your EC2 instance will go to CloudWatch
- You need to run a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permissions are correct
- EC2 Instance -> CloudWatch Logs Agent -> Cloudwatch Logs
- The cloudWatch log agent can be setup on premises too

# CloudWatch EventBridge (formerly CloudWatch Events)

- Schedule Cron jobs (schedule scripts)
  - Every hour -> Trigger script on Lambda funcions
- Event Pattern -> Event rules to react to a service doing something
  - IAM Root User Sign in Event -> SNS Topic with Email notification
- Trigger lambda functions, send SQS/SNS messages

- Example Source:
  - EC2 Instance (start instance)
  - CodeBuild (ex: failed build)
  - S3 Event (upload object)
  - Trusted Advisor (new Finding)
  - CloudTrail (any API call)
  - Schedule or Cron (every 4 hours)
- Source -> Amazon EventBridge -> Destination
- Example Destinations:
  - Lambda
  - AWS Batch
  - EC2 Task
  - SQS, SNS
  - Step functions...
- Events from AWS -> **Default Event Bus**
- Can react to events from AWS SaaS Partners -> **Partner Event Bus**
- React to Custom Apps -> **Custom Event Bus**

# AWS CloudTrail

- Provides Governance, compliance and audit for your AWS account
- CloudTrail is enabled by default
- Get an history of events / API calls made within your AWS account by:
  - console
  - SDK
  - CLI
  - AWS services
- Can put logs from CloudTrail into CloudWatch Logs or S3
- a trail can be applied to all Regions (default) or single region
- if a resource is deleted in AWS, investigate CloudTrail first

# AWS X-Ray

- Tooling to debug in production
- log analysis is hard when services are distributed (no common view of entire architecture)
- Visual analysis of our applications
- identify where the requests went wrong
- Troubleshooting performance
- understand dependencies in a microservice architecture
- Pinpoint service issues
- Review request behavior
- Find errors and exceptions
- Metting the SLA (Service Level Agreement)
- identify throttled
- identify users that are impacted

# Amazon CodeGuru

- An ML-powered service for automated code reviews and application performance recommendations
- Two functionalities
  - CodeGuru Reviewer: automated code reviews for static code analysis (development)
    - Identify critical issues, security, vulnerabilities, and hard-to-find bugs
    - Common coding best practices, resource leaks, security detection, input validation
    - uses ML and automated reasoning
    - Hard-learned lessons across millions of code reviews on 1000s open-source and Amazon repositories
    - Supports Java and Python
    - Integrates with GitHub, BitBucket, and AWS CodeCommit
  - CodeGuru Profiler: visibility/recommendations about application performance during runtime (production)
    - detect and optimize the expensive lines of code pre-prod
    - Identify performance and cost improvements in production
    - helps understand the runtime behavior of your application
    - identify if your application is consuming excessive CPU capacity on a logging routine
    - supports applications running on AWS or on-premise
    - minimal overhead on application

# AWS Health Dashboard

## Service History

- shows all regions, all services health
- shows historical information
- Has an RSS feed you can subscribe to

## Your Account

- Provides alerts and remediation guidance when AWS is experiencing events that may impact you
- Services Health Dashboard -> general status of AWS services
- Account Health Dashboard -> personalized view into the performance and availability of the AWS services underlying your AWS Resources
- the dashboard displays relevant and timely information to help you manage events in progress and provides proactive notification to help you plan for scheduled activities
- can aggregate data for entire AWS Organization
- Global services
- shows all AWS outages impact you and your AWS resources
- Alert, remediation, proactive, scheduled activities

# Summary

- CloudWatch
  - Metrics: monitor the performance of AWS Services and billing metrics
  - Alarms: automate notification, perform EC2 action, notify SNS based on metric
  - Logs: collect log files from EC2 instances, servers, Lambda Functions
  - Events (or EventBridge): react to events in AWS or trigger a rule on a schedule
- CloudTrail: audit API calls made within your AWS account
- CloudTrail insights: automated analysis of your CloudTrail Events
- X-Ray: trace requests made through your distributed applications
- AWS Health Dashboard: status of all AWS Services across all regions
- AWS Account Health Dashboard: AWS events that impact your infrastructure
- Amazon CodeGuru: automated code reviews and application performance recommendations
