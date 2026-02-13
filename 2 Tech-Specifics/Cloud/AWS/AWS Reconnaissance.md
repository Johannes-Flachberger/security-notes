---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/reconnaissance/passive"
---
# Fundamentals

While some enumeration techniques are specific to one service in AWS, many techniques are based on the interaction of multiple services.

**Attack Surface:**
- Large organisations might deliberately share resources between AWS accounts or even publicly.
- Sometimes, resources are shared by accident

> [!NOTE] This is "External Enumeration".
> While most techniques listed here require an AWS account, this can be any AWS account set up by the attacker. No initial compromise has been achieved yet.

# Pentesting

**Workflow:**
- See [[2 Tech-Specifics/Cloud/Cloud Reconnaissance|Cloud Reconnaissance]]

## Find public cloud ressources

### Basic Enumeration using AWS CLI

**Tool:** [[3 Tools/cloud/AWS CLI|AWS CLI]]

**Checklist:**
- [ ] Ressources that should be private to an organization, but are public
	- [ ] [Amazon Machine Images](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html) (AMIs)
		- [ ] There are AMIs provided by amazon, but organisations can have their custom prebuilt AMIs too, potentially revealing sensitive information
	- [ ] [Elastic Block Storage](https://aws.amazon.com/ebs/) (EBS) snapshots
	- [ ] [Relational Databases](https://aws.amazon.com/rds/) (RDS) snapshots

### Enumerate IAM identities in other AWS accounts

Using [cross-account access](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic-cross-account.html), an IAM identity within one account (the trusted account) can be granted access to a ressource in another account (the trusting account). When setting up cross-account-access, the trusting account receives information if the user of the trusted account has been found and successfully granted access.

You can abuse this feature to check if an IAM identity exists within another AWS account.

**Tools:**
- [[3 Tools/exploitation frameworks/pacu|pacu]]: automates the whole workflow
	- use modules from the `RECON_UNAUTH` module to enumerate various types of IAM identities

**Example Workflow:** enumerate IAM user identities manually
1. In the local account, create a resource to use for the enumeration.
	- e.g. an [[3 Tools/cloud/AWS CLI#Work with S3 buckets|create an S3 bucket]]
2. Create a [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals#IAM Policies|IAM Policy]] that grants a the target IAM user of the known target AWS account access to the resource
	- Note: IAM identities are identified using [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals#AWS Resource Name (ARN)|ARNs]]
- Attach the policy to the resource - if successful, the supposed IAM identity exists
	- e.g. [[3 Tools/cloud/AWS CLI#Work with S3 buckets|attach policy to S3 bucket]]

**Example policy for user enumeration:**

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowUserToListBucket",
            "Effect": "Allow",
            "Resource": "<ressource_ARN>",
            "Principal": {
                "AWS": ["<target_IAM_user_ARN"]
            },
            "Action": "s3:ListBucket"

        }
    ]
}
```

## Enumerate services for attack vectors

**See:**
- [[2 Tech-Specifics/Cloud/AWS/AWS S3 Buckets|AWS S3 Buckets]]

# Hardening
