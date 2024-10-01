# AWS Advanced Identity

## AWS STS - Security Token Service

- Enables you to create temporary, limited privileges credentials to access your AWS resources
- short term credentials: you configure expiration period
- Use Cases:
  - identity federation: manage user identities in external systems, and provide them STS tokens to access AWS resources
  - IAM Roles for cross/same account access
  - IAM Roles for Amazon EC2: provide temporary credentials for EC2 instances to access AWS resources

## Cognito

- provide identity for your Web and Mobile Applications users (potentially millions)
- instead of creating them an IAM user, your create a user in Cognito
- login with Facebook, Google...

## Microsoft Active Directory Services

- Found on any Windows Server with AD Domain Services
- Database of Objects: User Accounts, Computers, Printers, File Shares, Security Groups
- Centralized security, management, create account, assign permissions

## AWS Directory Services

- AWS Managed Microsoft AD
- AD Connector
- Simple AD

## AWS IAM Identity Center - successor to AWS Single Sign On

- one login for all your
  - AWS accounts in AWS Organizations
  - Business cloud applications
  - SAML2.0 enabled applications
  - EC2 Windows Instances
- identity providers
  - built-in identity store in IAM Identity Center
  - 3rd party: AD, OneLogin, Okta

## Summary

- IAM
  - Identity and Access Management inside your AWS account
  - For users that you trust and belong to your compary
- Organizations: manage multiple accounts
- Security Token Service (STS): temporary, limited-privileges credentials to access AWS resources
- Cognito: create a database of users for your mobile and web applications
- Directory Services: integrate Microsoft Active Directory in AWS
- IAM Identity Center: one login for multiple AWS accounts and applications
