---
tags:
  - "#type/tech-specific"
  - "#attack/discovery"
  - "#attack/credential-access"
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Fundamentals - Active Directory]]

# Pentesting

There are multiple tools for manual enumeration:

- [[#Enumeration with PowerView / SharpView]]: **most powerful option** - third party script, provides useful functions for manual
- [[#Enumeration with net.exe]]: built-in, only for very quick & basic user and group enumeration
- [[#Enumeration with PowerShell]]: uses built-in .Net Classes - more advanced enumeration

## Enumeration Checklist

- [ ] Groups
	- [ ] their properties, description and members can reveal privileged users
	- [ ] compare present groups with default groups: [Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups#default-security-groups)
	- [ ] eg. Domain Admin group
- [ ] Users
	- [ ] `pwdlastset,lastlogon`: reveal if the user is actively used or not --> impersonating inactive users might cause less friction
	- [ ] group membership
- [ ] Computers
	- [ ] OS Version
	- [ ] Server vs Client
	- [ ] hostname
- [ ] Relationships between Users, Computers, etc.
	- [ ] Privileges of users you already control on other hosts
	- [ ] Logged-on users on other hosts
- [ ] Cached credentials (use [[3 Tools/mimikatz|mimikatz]])
	- [ ] Password hashes
	- [ ] Kerberos tickets
- [ ] Service Accounts
	- [ ] might be members of privileged groups
	- [ ] Local default service accounts: [_LocalSystem_](https://learn.microsoft.com/en-us/windows/win32/services/localsystem-account), [_LocalService_](https://learn.microsoft.com/en-us/windows/win32/services/localservice-account), and [_NetworkService_](https://learn.microsoft.com/en-us/windows/win32/services/networkservice-account).
	- [ ] [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Service Principal Names (SPNs)]]
		- [ ] reveal host & port of the service
- [ ] Object permissions
	- [ ] reveals which users, service accounts, groups, etc. have certain permissions on objects - e.g. computers, shares, another user,...
	- [ ] this can be a major vector for privilege escalation
- [ ] file shares
	- [ ] can contain relevant documents, setup scripts, policy backups,...

## Enumeration with net.exe

### Enumerate Domain Users and Groups

| Purpose                                                                                                                                                             | Command                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| list domain users                                                                                                                                                   | `net user /domain`              |
| list details & privileges of a domain user                                                                                                                          | `net user <username> domain`    |
| list group details and members<br>**Hint:** only user objects are listed as group members, but no nested groups - to list nested groups, use PowerShell enumeration | `net group <groupname> /domain` |
| list groups                                                                                                                                                         | `net group /domain`             |
| list cached kerberos tickets                                                                                                                                        | `klist`                         |

Alternatively, use the [Get-ADUser](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-aduser?view=windowsserver2022-ps) Cmdlet (not preinstalled per default)

## Enumeration with PowerView / SharpView

See [[3 Tools/microsoft/PowerView & SharpView|PowerView & SharpView]]

> [!Hint] SYSVOL
> The [SYSVOL](https://learn.microsoft.com/en-us/archive/technet-wiki/24160.active-directory-back-to-basics-sysvol) share usually contains the domains group policies and scripts and is accessible by all domain users.
> - It is mapped to: `%SystemRoot%\SYSVOL\Sysvol\domain-name`
> - E.g: `\\dc1.mydomain.com\sysvol\mydomain.com\`
> 
> Sometimes, passwords are stored in policies, those are encrypted with AES-256 and a [known key from microsoft](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-gppref/2c15cbf0-f086-4c74-8b70-1f2fa45dd4be?redirectedfrom=MSDN#endNote2). Decrypt them on kali with `gpp-decrypt <encrypted_password>`

## Enumeration with PowerShell

Useful .Net classes for AD enumeration:

- [Domain Class](https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.activedirectory.domain?view=windowsdesktop-7.0): get basic domain info
- [DirectoryEntry](https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directoryentry?view=dotnet-plat-ext-6.0): searching
	- can be passed credentials for authentication
- [DirectorySearcher](https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher?view=dotnet-plat-ext-6.0): searching

The [Active Directory Service Interfaces (ADSI)](https://learn.microsoft.com/en-us/windows/win32/adsi/active-directory-service-interfaces-adsi) provide access to active directo

ry from [[3 Tools/shells/PowerShell|PowerShell]].

### Get LDAP path of domain controller

You can use the following snippet to build the LDAP path to the domain controller for the current domain:

```powershell
# Get PDC host name for current domain
$PDC = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().PdcRoleOwner.Name

# Get distinguished name of of the domain  
$DN = ([adsi]'').distinguishedName 

# Build & print the LDAP path
$LDAP = "LDAP://$PDC/$DN"
$LDAP
```

### Search objects within the AD

The argument to `DirectoryEntry` defines the object where the search is started.

```powershell
$direntry = New-Object System.DirectoryServices.DirectoryEntry($LDAP)
$dirsearcher = New-Object System.DirectoryServices.DirectorySearcher($direntry)
$dirsearcher.filter="<search filter>"
$searchResult = $dirsearcher.FindAll()
$searchResult
```

The search filter can match any property of the search results and uses [LDAP format](https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher.filter?view=windowsdesktop-10.0#system-directoryservices-directorysearcher-filter). For example:

- `name=testuser`
- `samAccountType=0x30000000`: specifies the type of the object, see [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/adschema/a-samaccounttype)
- `objectclass=group`: all groups
- `(&(objectCategory=group)(cn=<name>))`: groups with a specific name

Remove the filter to list all objects.

### List properties of all search results

```powershell

Foreach($obj in $searchResult)
{
    Foreach($prop in $obj.Properties)
    {
        $prop
    }

    Write-Host "---------------------------------------------------"
}
```

**Interesting properties:**

- `memberof`: groups the user is a memberof
- `member`: members of a group

## Other Tools

| Tool                                                      | Purpose                                                                                       |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| [[3 Tools/microsoft/Sysinternals#PsLoggedOn\|PsLoggedOn]] | list logged-in users on remote machine                                                        |
| `setspn -L <service user>`                                | list SPNs of a service account                                                                |
| [[3 Tools/mimikatz\|mimikatz]]                            | extract cached credentials, kerberos tickets,...<br>**Prerequisite:** Local Admin Permissions |

# Hardening
