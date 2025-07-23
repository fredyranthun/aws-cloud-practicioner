# EC2 Instance Metadata (IMDS)

- AWS EC2 Instance Metadata (IMDS) is powerful but one the least known features to developers
- it allows AWS EC2 instances to "learn about themselves" without using an IAM Role for that purpose
- You can retrieve the IAM Role name from the metadata, but you can not retrieve the IAM Policy
- Metadata = info about the EC2 instance
- Userdata = launch script of the EC2 instance

- Let's practice and see what we can do with it

## IMDSv2 vs IMDSv1

- IMDSv2 is more secure and is done in two steps
  - Get Session token - using headers and PUT
  - Use Session Token in IMDSv2 calls - using headers
