---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

# Pentesting

See [[1 Methods/Security-Testing/6 Privilege Escalation/Overview - 6 Privilege Escalation|Generic Strategy]] and [[1 Methods/Security-Testing/6 Privilege Escalation/Generic Privilege Escalation Checklist|Generic Privilege Escalation Checklist]].

**Workflow:**

1. Get an overview of the target - see [[2 Tech-Specifics/OS/Windows/Basic Enumeration - Windows|Basic Enumeration - Windows]].
2. If possible use [[#Automated Enumeration]], otherwise use [[#Manual Enumeration]].
3. Execute privilege escalation vectors: See [[2 Tech-Specifics/OS/Windows/Privilege Escalation - Windows/Privilege Escalation Vectors - Windows|Privilege Escalation Vectors - Windows]].
	- Note, that not all attack vectors that appear possible at first glance actually are possible.
4. Here, only some basic privesc methods are listed - also check [[#External Checklists & Ressources]]

## Automated Enumeration

> [!Warning] Warning
> Privilege escalation tools sometimes tend to miss stuff that can be revealed by in-depth manual enumeration, or to fail on attack vectors that are manually exploitable.

**See:**

- [[3 Tools/privilige escalation/winPEAS|winPEAS]]: on kali available as `peass`
	- winPEAS may not distinguish between Windows 10 and 11 correctly
- [[3 Tools/privilige escalation/PowerUp|PowerUp]]: includes an "AbuseFunction" for most vectors that can be run by the tool
- [[3 Tools/microsoft/Windows Exploit Suggester - Next Generation (WESNG)|Windows Exploit Suggester - Next Generation (WESNG)]]
- if you have a [[3 Tools/exploitation frameworks/Metasploit/meterpreter|meterpreter]] shell:
	- use `multi/recon/local_exploit_suggester`
- [Seatbelt](https://github.com/GhostPack/Seatbelt)
- [BeRoot](https://github.com/AlessandroZ/BeRoot)
- [JAWS](https://github.com/411Hall/JAWS)

**Note:** Each tool has strengths and weaknesses. Running multiple tools can rule out false positives and reveal additional attack vectors.

## Manual Enumeration

**See:** [[2 Tech-Specifics/OS/Windows/Privilege Escalation - Windows/Privilege Escalation Vectors - Windows|Privilege Escalation Vectors - Windows]]

## External Checklists & Ressources:

- [Payload all the things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)
- [HackTricks](https://book.hacktricks.wiki/en/windows-hardening/checklist-windows-privilege-escalation.html)

# Hardening
