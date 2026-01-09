---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

For windows privilege levels see [[2 Tech-Specifics/OS/Windows/Fundamentals Windows|Fundamentals Windows]].

During enumeration, never forget to cross-connect information to gather value. E.g. a running process that binds to port 443, that has an executable, configuration files, a specific software version, etc.

# Pentesting

If possible use [[#Tool-Based Enumeration]] (be aware of [[2 Tech-Specifics/OS/Antivirus Evasion|Antivirus Evasion]]).  
If automated enumeration is not possible, use [[#Manual Enumeration]].

## Workflow

1. Get an overview of the current system
2. Perform in-depth enumeration & carry out attacks

## Tool-Based Enumeration

> [!Warning] Warning
> Privilege escalation tools sometimes tend to miss stuff that can be revealed by in-depth manual enumeration, or to fail on attack vectors that are manually exploitable.

See:

- [[3 Tools/privilige escalation/winPEAS|winPEAS]]: on kali, available as `peass`
- [[3 Tools/privilige escalation/PowerUp|PowerUp]]: includes an "AbuseFunction" for most vectors that can be run by the tool
- [[3 Tools/windows/Windows Exploit Suggester - Next Generation (WESNG)|Windows Exploit Suggester - Next Generation (WESNG)]]
- if you have a [[3 Tools/exploitation frameworks/Metasploit/meterpreter|meterpreter]] shell:
	- use `multi/recon/local_exploit_suggester`
- [Seatbelt](https://github.com/GhostPack/Seatbelt)
- [BeRoot](https://github.com/AlessandroZ/BeRoot)
- [JAWS](https://github.com/411Hall/JAWS)

### Manual Enumeration

#### Overview

Generic Checklist: [[1 Methods/Security-Testing/6 Privilege Escalation/Generic Privilege Escalation Checklist|Generic Privilege Escalation Checklist]]

Cheat Sheet: [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Basic Enumeration Windows|Basic Enumeration Windows]]

#### In-depth

Start with: [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Basic Enumeration Windows|Basic Enumeration Windows]]

Then:

- [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Privilege Escalation Vectors Windows|Privilege Escalation Vectors Windows]]
- [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Service Hijacking|Service Hijacking]]

External Checklists & Ressources:

- [Payload all the things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)
- [HackTricks](https://book.hacktricks.wiki/en/windows-hardening/checklist-windows-privilege-escalation.html)

Further reading:

- <https://github.com/sagishahar/lpeworkshop>
- [HackTricks](https://book.hacktricks.wiki/en/windows-hardening/windows-local-privilege-escalation/index.html)

# Hardening
