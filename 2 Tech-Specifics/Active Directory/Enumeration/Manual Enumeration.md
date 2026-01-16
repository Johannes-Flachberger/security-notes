---
tags:
  - "#type/tech-specific"
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Fundamentals - Active Directory]]

# Pentesting

## Enumeration using legacy Windows Tools

### Enumerate Domain Users

| Purpose                                                                                                                                                                                 | Command                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| list domain use                                                                                                                                                                         | `net user /domain`               |
| list details & privileges of a domain u                                                                                                                                             er  | `net user <username> domain`     list groups<br>compare to default groups: [Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups#default-security-groups) ps:  | `net group /domain`              |
| list group members & de                                                                                                                                                                 | `net group <groupname> /domaiin` |

# Hardening
