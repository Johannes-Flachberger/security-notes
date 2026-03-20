---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
---
# Fundamentals

**See:**

- [Access Methods](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-bucket-intro.html)

# Pentesting

## Enumeration

### Discern further bucket names from naming convention

- analyse an already-known bucket name to discern other bucket names
	- often bucket names follow a naming convention
	- often bucket names include a short random part, since they must be unique accross a region - maybe organisations share the same random part accross all their buckets?

### Check access to the bucket

#### Using the S3 RestAPI

**Using the S3 REST API:**

- browse the bucket root
- e.g. `http://domain/bucket_name`

**Using [[3 Tools/cloud/AWS CLI|AWS CLI]]:**

- use a set of valid credentials to authenticate to an AWS account
	- e.g. of captured credentials or of any other AWS account
- list bucket contents - see [[3 Tools/cloud/AWS CLI#Work with S3 buckets|AWS CLI - Work with S3 buckets]]

> [!Hint] Hint
> Sometimes, private buckets have the "AuthenticatedUsers" policy set, which grants access to any authenticated user with ANY AWS account. --> Using [[3 Tools/cloud/AWS CLI|AWS CLI]], even private buckets might be accessible.

### Enumerate Bucket Contents

If you don't have full read access to a bucket, you can try to enumerate its contents using [[2 Tech-Specifics/Web/Enumeration - Web/Overview - Enumeration - Web#Directory Enumeration|Directory Enumeration]]

### Enumerate OwnerId using readable S3 bucket

Obtain the Account ID of the bucket owner.

**Prerequisites:**

- Permission to read on object within a bucket (`s3:getObject`) or to list the buckets contents (`s3:ListBucket`)
- any AWS account to interact with the [[2 Tech-Specifics/Cloud/AWS/AWS API|AWS API]]

**Tool:** [s3-account-search](https://github.com/WeAreCloudar/s3-account-search)

- Automates the whole workflow.
- Uses IAM role identities instead of IAM user identities for the condition based enumeration.

**Workflow:**

1. Create new IAM user identity in the attacker account (by default it does not have any permissions)
	- See [[3 Tools/cloud/AWS CLI#Manage Users and Policies|Manage users with AWS CLI]]
2. Add a policy, to grant permissions to list buckets & read objects if the `OwnerId` starts with digit `x`.
3. Test access to the bucket with digits 0-9 --> first digit of the `OwnerId` obtained
4. Perform the steps for all digits within the `OwnerId`

**Note:** Policies need some time to become active, so between each test you should wait ~10 seconds.

**Example Policy as starting point:**

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowResourceAccount",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": "*",
            "Condition": {
                "StringLike": {"s3:ResourceAccount": ["0*"]}
            }
        }
    ]
}
```

## Exfiltration

Download data to local machine using [[3 Tools/cloud/AWS CLI#Work with S3 buckets|AWS CLI - Work with S3 buckets]]

It might be more stealthy to transfer data to another S3 bucket than to download it to a local machine (i.e. to the outside of the cloud environment).

# Hardening
