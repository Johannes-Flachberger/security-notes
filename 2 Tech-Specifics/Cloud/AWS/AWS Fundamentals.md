---
tags:
  - "#type/tech-specific"
---
# Services

**Cloudtrail:** Monitoring Service of AWS

# Basic concepts

## AWS Resource Name (ARN)

See [Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference-arns.html)

Amazon Resource Names (ARNs) uniquely identify AWS resources. ARNs of [[#IAM identities]] include the account id, the identity type and the name.

- e.g. ARN of a user: `arn:aws:iam::<account_id>:user/<user_name>`
- e.g. ARN of a bucket: `arn:aws:s3:::<bucket_name>`

In ARNs, [paths](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-friendly-names) can be used to group identities - e.g. `user/it_support/joe`. Permissions can be granted based on paths.

# IAM

## Accounts vs. IAM IDs

An AWS Account is a "top-level entity" that groups ressources, and is used for **billing**.

Within an AWS Account, using the AWS IAM, many different users, roles and groups can be created, which are called AWS IAM identities.

## IAM Policies

There are two types of policies:

- **Managed Policies:** Dinstinct, re-usable objects, can be assigned to many identities.
	- AWS also provides ["AWS Managed Policies"](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/about-managed-policy-reference.html). - Those are pre-defined by AWS and often over-permissive
		- **If used alone, they are a security risk / possible attack surface.**
		- Their ARN has the following schema: `arn:aws:iam::aws:policy/<PolicyName>`
- **Inline Policies:** Directly assigned to a single identity, not re-usable.

Policies can be inherited, e.g. based on the ARN path or the group of an identity.

### Inline Policies

AWS IAM policies use a specific json format.

**See:**

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

## IAM identities

### Roles

A role is an entity that grants a set of privileges to a user. Users dont "hold" a role per default, but instead they can "assume" a role if they have the permissions to do so.

When assuming a role the [[2 Tech-Specifics/Cloud/AWS/AWS API|AWS API]] / [[3 Tools/cloud/AWS CLI|AWS CLI]] returns a set of temorarily valid credentials that, when used provide the privileges specified by the role.
