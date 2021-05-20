---
description: How to authenticate with AWS provider
---

# Authentication

You should be authenticated with an AWS account with correct permission with either option \(see full [documentation](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html)\):

* `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`
* `~/.aws/credentials` created via `aws configure`
* `AWS_PROFILE`

Multi-account AWS support is available by using an account which can [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) to other accounts.

In your `config.yml` you need to specify one or more`role_arn` if you want to query multiple accounts in the following way:

```yaml
 accounts:
     - role_arn: <arn>
```

