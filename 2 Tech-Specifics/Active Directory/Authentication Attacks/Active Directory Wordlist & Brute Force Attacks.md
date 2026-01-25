---
tags:
  - "#type/tech-specific"
---
# Fundamentals

See:

- [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Fundamentals - Active Directory]]
- [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]]

# Pentesting

> [!Warning] Prevent Account Lockouts
> As account lockouts create a) friction within the target organization and b) may raise alarms, they should be prevented.

## Prevent Account Logouts

Use `net accounts` to show the account policy.

Important entries are:

- `Lockout threshold`
- `Lockout duration (minutes)`
- `Lockout observation window (minutes)`

## Password Attacks using AD queries

 Make a query against the domain controller using specified credentials with[DirectoryEntry](https://docs.microsoft.com/en-us/dotnet/api/system.directoryservices.directoryentry?view=dotnet-plat-ext-6.0). DirectoryEntry creates a PowerShell object referencing an object in the directory, using the provided credentials.

See [[2 Tech-Specifics/Active Directory/Enumeration/Manual Enumeration - Active Directory#Get LDAP path of domain controller|Manual Enumeration - Active Directory]] to build the `$LDAPPath`.

```powershell
New-Object System.DirectoryServices.DirectoryEntry($LDAPPath, "<user>", "<password>")
```

The [Spray-Passwords script](https://github.com/michele-dedonno/MDD-scripts/blob/master/Spray-Passwords.ps1) automates this process, respecting the account policy + it checks if the account is a local admin user.

## Password Attacks using SMB

**Note:** [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]] is a lot noisier than DirectoryServices queries.

**Tools:**
- [[3 Tools/bruteforce/netexec|netexec]]

## Kerberos

See [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Brute Force / Dictionary|Kerberos]]

# Hardening
