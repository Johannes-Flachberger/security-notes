---
tags:
  - "#type/tool"
Link: "-"
Purpose:
---
# Info

A script / C# application that provides useful functions for manual active directory enumeration.

PowerView is the original PowerShell implementation. SharpView is a C# implementation of PowerView.

Both implementations are not longer supported, but still useful today.

**Links:**

- [PowerView Repo](https://github.com/PowerShellMafia/PowerSploit/blob/dev/Recon/PowerView.ps1)
- [SharpView Repo](https://github.com/tevora-threat/SharpView)

# Usage

> [!Warning] Cryptic errors
> The produced errors, e.g. in case of an authentication failure can be quite cryptic.

**Hint:**

Depending on the context (e.g. if a [[2 Tech-Specifics/Network/Protocols/Kerberos|Kerberos]] TGT is already cached), you might need to pass credentials usign `-Credential <user>@<domain>/<passwor>`.

**Usage:**

1. Import script into scope: `Import-Module .\PowerView.ps1`
2. Run Powerview Commands

- Filter results with `| Where-Object { $_.<property> -eq <value>}`
- Filter properties to show in results: `| select <property>`.

**Function Reference:** [PowerView Docs](https://powersploit.readthedocs.io/en/latest/Recon/)

### Basic Enumeration

| Command                                                             | Purpose                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-Domain`                                                        | show basic information about the current domain                                                                                                                                                                                                                                                                                                                              |
| `Get-DomainUser`                                                    | list all users                                                                                                                                                                                                                                                                                                                                                               |
| `Get-DomainGroup`                                                   | list all groups                                                                                                                                                                                                                                                                                                                                                              |
| `Get-DomainComputer`                                                | list details of computers<br>e.g. filter for `operatingsystem, operatingsystemversion, dnshostname`                                                                                                                                                                                                                                                                          |
| `Find-LocalAdminAccess`                                             | list hosts where the current user has local admin privileges<br>based on the [OpenServiceW function](https://learn.microsoft.com/en-us/windows/win32/api/winsvc/nf-winsvc-openservicew)                                                                                                                                                                                      |
| `Get-NetSession -ComputerName <hostname> -Verbose`                  | list currently logged on users on remote machine<br>based on [NetWkstaUserEnum](https://learn.microsoft.com/en-us/windows/win32/api/lmwksta/nf-lmwksta-netwkstauserenum) (requires local admin privileges) and [NetSessionEnum](https://learn.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum)<br>**Note:** Does not work on modern windows systems. |
| `Get-DomainUser -SPN \| select samaccountname,serviceprincipalname` | list all SPNs - see [[2 Tech-Specifics/Active Directory/Fundamentals - AD\|Fundamentals - Active Directory]]                                                                                                                                                                                                                                                   |

**Note:** [NetSessionEnum](https://learn.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum) relies on the `HKLM:SYSTEM\CurrentControlSet\Services\LanmanServer\DefaultSecurity\SrvsvcSessionInfo` registry key work (permissions on this key could also be set to a non-default value)

### Enumerate Object permissions

Relevant access rights & fundamentals: [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Object permissions|Fundamentals - Object Permissions]]

List permissions for a specific object:

- `Get-ObjectAcl -Identity <samaccountname>`

Filter for the most important properties:

- `| select SecurityIdentifier,ActiveDirectoryRights`

**List all access rights of a certain type that one object has on another:**

**Hint:** Remove the identity filter to show all objects that have a certain right on any other object.

```powershell
Get-ObjectAcl -Identity "<samaccountname>" | ? {$_.ActiveDirectoryRights -eq "<access_right>"} | select SecurityIdentifier,ActiveDirectoryRights
```

**Hint:** The `GenericAll` permission should be reserved for domain admins only.

Use `Convert-SidToName` to make [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|SID]]s readable.

**Print all Security Identifiers in readable format:**

```powershell
Foreach($ACE in $ACEs)
    {
        $ACE.ObjectSID | Convert-SidToName -ErrorAction SilentlyContinue
        $ACE.ActiveDirectoryRights
        $ACE.SecurityIdentifier | Convert-SidToName
        Write-Host "---------------------------------------------------"
    }

```

### Enumerate File Shares

| Command                   | Purpose                                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| `Find-DomainShare`        | List file shares<br>`-CheckShareAccess` to only list shares readable be the current user |
| `ls \\<hostname>\<share>` | Access file shares                                                                       |
| `Invoke-FileFinder`       | To search for sensitive files                                                            |

Use e.g. `| Format-List` if names are cut off.

# Snippets
