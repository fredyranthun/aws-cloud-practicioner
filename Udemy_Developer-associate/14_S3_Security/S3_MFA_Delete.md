## MFA S3 - MFA Delete

- MFA (Multi-Factor Authentication) - force users to generate a code on a device (usually a mobile phone or a hardware)
- MFA will be required to:
  - Permanently delete an object version
  - Suspend Versioning on the bucket
- MFA won't be required to:
  - Enable versioning
  - list deleted versions
- To use MFA Delete, versioning must be enabled on the bucket
- Only the bucket owner (root account) can enable/disable MFA delete
