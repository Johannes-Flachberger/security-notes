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

| Option                                                              | Purpose                                                                                                    |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `--profile <name>`                                                  | run command with a profile                                                                                 |
| option: `--filters "Name=<attribute>,Values=<value1>,[value2],..."` | filter results by attribute<br>e.g. filter by keywords in `description` or `name` using `*` as wildcard    |
| `--output <format>`                                                 | output format - see [Reference](https://docs.aws.amazon.com/cli/v1/userguide/cli-usage-output-format.html) |
| `aws <command> help` or<br>`aws <command> <sub-command> help`       | show help for a command or sub-command.                                                                    |

#### Work with named profiles

When creating a profile, you need to provide credentials, a default region and a default output format. If in doubt, just choose `us-east-1` as the default region.

**Hint:** You can also set a default profile in `~/.aws/config` or use `set AWS_DEFAULT_PROFILE=<profile_name>` to set a named profile as default

| Command                          | Purpose                                                                                       |
| -------------------------------- | --------------------------------------------------------------------------------------------- |
| `aws configure --profile <name>` | create new named profile within the CLI. It corresponds with a user in AWS IAM                |
| `aws sts get-caller-identity`    | get UserId, AccountId and ARN of the present<br>add `--profile <name>` to check a profile<br> |

#### Manage users and Policies

| Command                                                                                                  | Purpose                                                                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `aws iam create-user --user-name <name>`                                                                 | create new IAM user identity                                                                                                                                                                   |
| `aws iam create-access-key --user-name <name>`                                                           | create credentials for an IAM user identity                                                                                                                                                    |
| `aws iam put-user-policy --user-name <target_user> --policy-name <name> --policy-document file://<path>` | apply inline-policy to an IAM user<br>no output = sucess<br>See: [Reference](https://docs.aws.amazon.com/cli/latest/reference/iam/put-user-policy.html)<br>`--policy-document` must be a valid |

#### Work with S3 buckets

| Command                                                                     | Purpose                                                                                                                  |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| e.g. `aws s3 mb s3://<bucket_name>-$RANDOM-$RANDOM-$RANDOM`                 | create an s3 bucket with the specified name and random integer values to ensure uniqueness                               |
| `aws s3api put-bucket-policy --bucket <bucket_name> --policy file://<path>` | attach a [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals#IAM Policies\|IAM Policy]] to an S3 bucket<br>no output = success |
| `aws s3 ls <bucket_name>`                                                   | list contents of bucket                                                                                                  |
|                                                                             |                                                                                                                          |

#### Enumerate AMIs

**Command:** `aws ec2 describe-images`

| Option                   | Purpose                                                                |
| ------------------------ | ---------------------------------------------------------------------- |
| `--owners <owner_alias>` | filter by owner account id, or use e.g. `amazon` for AWS provided AMIs |
| `--executable-users all` | filter for all public AMIs                                             |

#### Enumerate EBS snapshots

**Command:** `aws ec2 describe-snapshots`

| Option             | Purpose                    |
| ------------------ | -------------------------- |
| `--owner-ids <id>` | filter by owner account id |

#### Enumerate RDS snapshots

**Command:** `aws rds describe-db-snapshots`

# Snippets
