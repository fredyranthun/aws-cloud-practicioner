## AWS CLI Profiles

- dealing with more than one account in your local machine

## AWS CLI with MFA

- to use MFA with the CLI, you must create a temporary session
- to do so, you must run the STS GetSessionToken API call

- aws sts get-session-token --serial-number -arn-of-the-mfa-device --token-code code-from-token --duration-seconds 3600

