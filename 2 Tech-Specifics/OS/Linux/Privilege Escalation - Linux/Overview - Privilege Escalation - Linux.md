---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

See [[1 Methods/Security-Testing/6 Privilege Escalation/Overview - 6 Privilege Escalation|Overview - 6 Privilege Escalation]] for a generic strategy.

# Pentesting

See [[1 Methods/Security-Testing/6 Privilege Escalation/Overview - 6 Privilege Escalation|Generic Strategy]] and [[1 Methods/Security-Testing/6 Privilege Escalation/Generic Privilege Escalation Checklist|Generic Privilege Escalation Checklist]].

**Workflow:**

1. Get an overview of the target: [[2 Tech-Specifics/OS/Linux/Basic Enumeration - Linux|Basic Enumeration - Linux]]
2. If possible, use [[#Automated Enumeration]]. If not use [[#Manual Enumeration]].
3. Execute a privilege escalation vector - see [[2 Tech-Specifics/OS/Linux/Privilege Escalation - Linux/Privilege Escalation Vectors - Linux|Privilege Escalation Vectors - Linux]]
4. Here, only some basic privesc methods are listed - also check [[#External Checklists & Resources]]

## Automated Enumeration

**Tools:**

- [[3 Tools/privilige escalation/linpeas|linpeas]]
- [[3 Tools/privilige escalation/lse|lse]]
- [[3 Tools/privilige escalation/LinEnum|LinEnum]]
- [unix-privesc-check](https://pentestmonkey.net/tools/audit/unix-privesc-check)
- [LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester)
- [Linux Priv Checker](https://github.com/linted/linuxprivchecker)

**Note:** Each tool has strengths and weaknesses. Running multiple tools can rule out false positives and reveal additional attack vectors.

## Manual Enumeration

Perform detailed enumeration and execute an attack vector: [[2 Tech-Specifics/OS/Linux/Privilege Escalation - Linux/Privilege Escalation Vectors - Linux|Privilege Escalation Vectors - Linux]]

## External Checklists & Resources

- [HackTricks](https://book.hacktricks.wiki/en/linux-hardening/linux-privilege-escalation-checklist.html)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)
- [g0tmi1k](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
- [TotalOSCPGuide](https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html)

# Hardening
