# IAM - Identity and Access Management

- It is a global service
- By default, the root account is created and must be used only for setting up the other accounts
- Users are people in your organization and they can be grouped
- Groups contain only users, not other groups
- Users do not have to belong to groups, and can be belong to more than one group
- users and groups can be assigned JSON documents called Policies

## Policy example

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    }
  ]
}
```

- defines the permissions of the users
- can allow users or groups to do certain actions
- in AWS you apply the least privilege principle: don't give more permission than one needs

- when attaching a policy to a group, it is attached to the users whithin that group
- generally this way is more recommended

## Creating a new user

- to login, use the url of the account (can use with an alias)
- attach the Administrator policies to a group, and then add the user to that group

## IAM Policies Inheritance

- a user can be in more than one group, or receive inline policies (directly for the user)
- IAM policies consists of:
  - Version
  - Id: optional identifier to that policy
  - One or more statements
- Statements consists of:
  - Sid: identifier of the statement (optional)
  - Effect: "allow" or "deny"
  - Principal: account/user/role to which this policy applied to
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions applied to
  - Condition: optional, when this policy is in effect
