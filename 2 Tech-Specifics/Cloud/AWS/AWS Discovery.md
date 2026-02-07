---
tags:
  - "#type/tech-specific"
  - "#attack/discovery"
---
# Fundamentals

After an initial compromise of the AWS target environment, by e.g. obtaining an access token, you'll need to get oriented within the environment.

**See:**

- [[1 Methods/Security-Testing/9 Discovery/Overview - 9 Discovery|Overview - 9 Discovery]]
- [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals|AWS Fundamentals]]

> [!Warning] Be stealthy!
> Since logging is enabled by default by popular cloud providers, it is important to stay stealthy during discovery. It makes sense to initially check the present privileges and keep actions within those privileges.

# Pentesting

**Workflow:** See [[2 Tech-Specifics/Cloud/Cloud Discovery|Cloud Discovery]]

## Examine obtained Credentials

**Tool:** [[3 Tools/cloud/AWS CLI|AWS CLI]]

| Command                                                              | Purpose                                                                                                                                                                                                                              |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `aws sts get-caller-identity`                                        | Show UserId, AccountId and ARN of the present credentials (i.e. access key & secret access key)<br>**Note:** This is **always works**, even if permissions are explicitely denied, but its also **always logged**.                   |
| `aws sts get-access-key-info`                                        | Show Account ID of the supplied access key - good to check if the access key is in scope of the assessment                                                                                                                           |
| `aws lambda invoke --function-name <function_name_or_arn> <outfile>` | Provides ARN of the used identity.<br>Execute a non-existent lambda function and retrieve information from the error message.<br>The `<outfile>` argument does not really matter in this case<br>This is **not logged per default**. |

**Hint:** Often, accounts permit the use of more regions than are actually used and monitored. Depending on the quality of the monitoring setup of the target account, it can help to issue commands in a different region than is usually used by the AWS account, to evade detection.  

## Enumerate Permissions of the obtained Identity

There are 2 main ways:

- If you have permissions to query the IAM: [[#Enumerate Identity Policies using IAM]]
- Otherwise: [[#Brute-force permissions]]

### Enumerate Identity Policies using IAM

**Fundamentals:** [[2 Tech-Specifics/Cloud/AWS/AWS Fundamentals#IAM Policies|AWS Fundamentals]]

**See:** [[2 Tech-Specifics/Cloud/AWS/AWS IAM#Enumerate Identity Policies|AWS IAM]]

**Hint:** You can also make assumptions based on the path & name in the ARN of the identity.

### Brute-force permissions

> [!Warning] This is noisy & takes time.

**Tools:**
- [[3 Tools/exploitation frameworks/pacu|pacu]] modules:
	- `iam__bruteforce_permissions`

## Enumerate Accessible Resources

Enumerate Information about the resources you have permissions for.

Two options:

- **Automated enumeration:** There are many tools - creates a lot of noise.
- **Manual enumeration:** More targeted than automated enumeration, better if stealthiness is required.

**See:**
- Get Account Overview using [[2 Tech-Specifics/Cloud/AWS/AWS IAM#Get Account Overview|AWS IAM]]
- Use [[2 Tech-Specifics/Cloud/AWS/AWS IAM|AWS IAM]] to enumerate policies for other users.

# Hardening
