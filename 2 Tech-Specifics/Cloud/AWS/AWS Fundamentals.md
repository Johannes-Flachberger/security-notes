---
tags:
  - "#type/tech-specific"
---
# IAM

## Accounts vs. IAM IDs

An AWS Account is a "top-level entity" that groups ressources, and is used for **billing**.

Within an AWS Account, using the AWS IAM, many different users, roles and groups can be created, which are called AWS IAM identities.

## IAM Policies

AWS IAM policies use a specific json format.

See:

- [Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html)
- [Json Policies Structure](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#access_policies-json)

**Example Policy:**

```json
{
  "Version":"2012-10-17",		 	 	 
  "Statement": {
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::amzn-s3-demo-bucket"
  }
}
```

## AWS Resource Name (ARN)

See [Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference-arns.html)

Amazon Resource Names (ARNs) uniquely identify AWS resources.

- e.g. ARN of a user: `arn:aws:iam::<account_id>:user/<user_name>`
- e.g. ARN of a bucket: `arn:aws:s3:::<bucket_name>`

## IAM identities

## Roles

A role is an entity that grants a set of privileges to a user. Users dont "hold" a role per default, but instead they can "assume" a role if they have the permissions to do so.

When assuming a role the [[2 Tech-Specifics/Cloud/AWS/AWS API|AWS API]] / [[3 Tools/cloud/AWS CLI|AWS CLI]] returns a set of temorarily valid credentials that, when used provide the privileges specified by the role.
