---
tags:
  - "#type/tool"
Link: https://docs.aws.amazon.com/cli/latest/
Purpose: remote management for AWS cloud resources
---
# Info

Uses the [[2 Tech-Specifics/Cloud/AWS/AWS API|AWS API]] to manage AWS resources

**Hint:** Profiles and credentials are stored in `~/.aws/` per default.

# Usage

> [!Hint] Official Reference: https://docs.aws.amazon.com/cli/latest/
> The official reference of AWS CLI is very good - this cheat sheet only lists the most used snippets.

#### Generic Options

| Option                                                              | Purpose                                                                                                                                                                                                                                |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--profile <name>`                                                  | run command with a profile                                                                                                                                                                                                             |
| option: `--filters "Name=<attribute>,Values=<value1>,[value2],..."` | filter results by attribute<br>e.g. filter by keywords in `description` or `name` using `*` as wildcard<br>**Note:** filters are evaluated server-side                                                                                 |
| `--query "<JMESPath_expression"`                                    | query the output using [[3 Tools/utilities/JMESPath and JP\|JMESPath]]<br>**Note:** queries are evaluated client-side<br>**See:** [AWS Docs](https://docs.aws.amazon.com/cli/v1/userguide/cli-usage-filter.html#cli-usage-filter-client-side) |
| `--output <format>`                                                 | output format - see [Reference](https://docs.aws.amazon.com/cli/v1/userguide/cli-usage-output-format.html)                                                                                                                             |
| `aws <command> help` or<br>`aws <command> <sub-command> help`       | show help for a command or sub-command.                                                                                                                                                                                                |

#### Work with named profiles

When creating a profile, you need to provide credentials, a default region and a default output format. If in doubt, just choose `us-east-1` as the default region.

**Note:** All configs are stored at `~/.aws/config`

| Command                             | Purpose                                                                                       |
| ----------------------------------- | --------------------------------------------------------------------------------------------- |
| `aws configure --profile <name>`    | create new named profile within the CLI. It corresponds with a user in AWS IAM                |
| `aws sts get-caller-identity`       | get UserId, AccountId and ARN of the present<br>add `--profile <name>` to check a profile<br> |
| `export AWS_PROFILE=<profile_name>` | set a default named profile                                                                   |

#### Manage Users and Policies

| Command                                                                                                  | Purpose                                                                                                                                                                                         |
| -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `aws iam create-user --user-name <name>`                                                                 | create new IAM user identity                                                                                                                                                                    |
| `aws iam create-access-key --user-name <name>`                                                           | create access key for an IAM user identity                                                                                                                                                      |
| `aws iam put-user-policy --user-name <target_user> --policy-name <name> --policy-document file://<path>` | attach inline-policy to an IAM user<br>no output = sucess<br>See: [Reference](https://docs.aws.amazon.com/cli/latest/reference/iam/put-user-policy.html)<br>`--policy-document` must be a valid |
| `aws iam attach-user-policy --user-name <username> --policy-arn <arn>`                                   | attach managed policy to an IAM user<br>e.g. ARN of the "admin" policy: `arn:aws:iam::aws:policy/AdministratorAccess`                                                                           |

#### Work with S3 buckets

| Command                                                                     | Purpose                                                                                                                  |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| e.g. `aws s3 mb s3://<bucket_name>-$RANDOM-$RANDOM-$RANDOM`                 | create an s3 bucket with the specified name and random integer values to ensure uniqueness                               |
| `aws s3api put-bucket-policy --bucket <bucket_name> --policy file://<path>` | attach a [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals#IAM Policies\|IAM Policy]] to an S3 bucket<br>no output = success |
| `aws s3 ls`                                                                 | list S3 buckets                                                                                                          |
| `aws s3 ls <bucket_name>`                                                   | list contents of bucket                                                                                                  |
| `aws s3 cp s3://<bucket_name>/<file_name> <local_dir>`                      | download files from bucket                                                                                               |
| `aws s3 sync s3://<bucket_name> <local_dir>`                                | copy all contents of a bucket to another location                                                                        |

#### Work with EC2 instances

| Command                      | Purpose                                                                                                                                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `aws ec2 describe-instances` | list EC2 instances                                                                                                                                                       |
| `aws ec2 describe-snapshots` | list EBS snapshots<br>`--owner-ids <id>`: filter by owner account id                                                                                                     |
| `aws ec2 desrcribe-images`   | list AMIs<br>`--owners <account_id>`: filter by owner account id, or use e.g. `amazon` for AWS provided AMIs<br>`--executable-users all`: filter for all public AMIs<br> |

#### Work with RDS Databases

| Command                         | Purpose            |
| ------------------------------- | ------------------ |
| `aws rds describe-db-snapshots` | list RDS snapshots |

#### Work with Lambda Functions

| Command                     | Purpose               |
| --------------------------- | --------------------- |
| `aws lambda list-functions` | list lambda functions |

# Snippets
