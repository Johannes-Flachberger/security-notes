---
tags:
  - "#type/tech-specific"
  - "#attack/discovery"
  - "#attack/persistence"
---
# Fundamentals

**See:** [[2 Tech-Specifics/Cloud/AWS/Fundamentals - AWS|Fundamentals - AWS]]

# Pentesting

## Discovery

**Tools:**
- Manual Enumeration: [[3 Tools/cloud/AWS CLI|AWS CLI]]
- Automated Enumeration: [[3 Tools/exploitation frameworks/pacu|pacu]]

**Hint:** Especially check for [[2 Tech-Specifics/Cloud/AWS/Fundamentals - AWS#IAM Policies|AWS Managed Policies]] as they might pose a security risk.

### Get Account Overview

Get an overview of the target account - its users, groups, policies etc. E.g. look for users with high privileges in order to impersonate them later.

> [!Hint] Stealthy enumeration
> To be stealthy, best collect as much information as possible with few commands and then analyse it offline. e.g. use `aws iam get-account-authorization-details` and then use [[3 Tools/utilities/JMESPath and JP|jp]].

**Automated Tools:**
- [[3 Tools/microsoft/BloodHound|BloodHound]] using the [IAMhounddog](https://bloodhound.specterops.io/opengraph/library#iamhounddog) ingestor.
	- Requires an AWS principal with either SecurityAudit or ReadOnlyAccess.
- [[3 Tools/exploitation frameworks/pacu|pacu]] modules: `iam__enum_users_roles_policies_groups`

| Command                                                               | Purpose                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `aws iam get-accunt-summary`                                          | get overview of the account, such as number of:<br>- policies<br>- users<br>- groups<br>- MFADevices<br>- MFADevicesInUse<br>- Roles<br>- Identity Providers<br><br>                                                                                                                                                                              |
| `aws iam list-users`<br>`aws iam list-groups`<br>`aws iam list-roles` | list users, groups and roles in the account                                                                                                                                                                                                                                                                                                       |
| `aws iam list-policies --scope Local --only-attached`                 | list all attached managed policies within the account - follow up with [[#Retrieve policy information]]                                                                                                                                                                                                                                           |
| `aws iam get-account-authorization-details`                           | list information about all IAM identities, policies and their relationships<br>use `--filter <type> [type] ...` to choose with identity types should be listed - see [Reference](https://docs.aws.amazon.com/cli/latest/reference/iam/get-account-authorization-details.html#options)<br>**Stealthy:** lists a lost of info with only one request |

### Enumerate Identity Policies

**Automated tools:**
- [[3 Tools/exploitation frameworks/pacu|pacu]] module: module `iam__enum_permissions`

#### List Policies and group memberships of a user

| Command                                                  | Purpose                                  |
| -------------------------------------------------------- | ---------------------------------------- |
| `aws iam list-user-policies --user-name <name>`          | list a users inline-policies             |
| `aws iam list-attached-user-policies --user-name <name>` | list managed policies attached to a user |
| `aws iam list-groups-for-user --user-name <name>`        | list group memberships of a user         |

#### List policies for a group

| Command                                                    | Purpose                                   |
| ---------------------------------------------------------- | ----------------------------------------- |
| `aws iam list-group-policies --group-name <name>`          | list a groups inline-policies             |
| `aws iam list-attached-group-policies --group-name <name>` | list managed policies attached to a group |

#### Retrieve policy information

| Command                                                           | Purpose                                                    |
| ----------------------------------------------------------------- | ---------------------------------------------------------- |
| `aws iam list-policy-versions --policy-arn <arn>`                 | Retrieve policy version                                    |
| `aws iam get-policy-version --policy-arn <arn> --version-id <id>` | Retrieve the policy document for a specific policy version |
**Hint:** Once you retrieved a policy, you can [[3 Tools/utilities/grep|grep]] the [[3 Tools/cloud/AWS CLI|AWS CLI]] help output for the allowed actions. E.g. `aws iam help | grep -E "list-|get-"`

## Persistence

If you have the necessary privileges, add a user - see [[3 Tools/cloud/AWS CLI#Manage Users and Policies|AWS CLI - Manage Users and Policies]]

# Hardening
