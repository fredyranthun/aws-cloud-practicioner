## AWS Limits (Quotas)

- API Rate Limits

  - DescribeInstances API for EC2 has a limit of 100 calls per second
  - GetObject on S3 has a limit of 5500 GET per second per prefix
  - For Intermittent Errors: implement Exponential Backoff
  - For Consistent Errors: request an API throttling limit increase

- Service Quotas (Service Limits)
  - Running On-Demand Standard Instances: 1152 vCPU
  - you can request a service limit increase by **opening a ticket**
  - you can request a service quota increase by using the **Service Quotas API**

## Exponential Backoff (any AWS Service)

- if you get **ThrottlingException** intermittently, use exponential backoff
- retry mechanism already included in AWS SDK API calls
- must implement yourself if using the AWS API as-is or in specific cases
  - must only implement the retries on 5xx server errors and throttling
  - do not implement on the 4xx client errors
