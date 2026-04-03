---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

# Pentesting

If possible, use [[#Automated Enumeration]]. If not use [[#Manual Enumeration]].

## Automated Enumeration

**Tools:**

- [[3 Tools/privilige escalation/lse|lse]]
- [[3 Tools/privilige escalation/LinEnum|LinEnum]]
- [[3 Tools/privilige escalation/linpeas|linpeas]]

## Manual Enumeration

- Generic Checklist: [[1 Methods/Security-Testing/6 Privilege Escalation/Generic Privilege Escalation Checklist|Generic Privilege Escalation Checklist]]
- Cheat Sheet: [[2 Tech-Specifics/OS/Linux/Manual Enumeration - Linux|Manual Enumeration - Linux]]

**External Checklists & Resources**

- [HackTricks](https://book.hacktricks.wiki/en/linux-hardening/linux-privilege-escalation-checklist.html)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)
- [g0tmi1k](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
- [TotalOSCPGuide](https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html)

# Hardening

# Scripts

scripts for privesc enumeration:

- [LinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - best tool
- [LinEnum](https://github.com/rebootuser/LinEnum)
- [unix-privesc-check](https://pentestmonkey.net/tools/audit/unix-privesc-check)
- [LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester)
- [Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
- [Linux Priv Checker](https://github.com/linted/linuxprivchecker)

**Note:** Each tool has strengths and weaknesses. Running multiple tools can rule out false positives and reveal additional attack vectors.

# Vectors:
