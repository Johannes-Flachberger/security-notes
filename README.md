These are my personal notes about cyber security. I collect know how from many different sources and try to summarize that here in a structured way. Of course, this will never be complete or perfect, so its always work in progress. Have Fun :)
# Philosophy
The goal of this knowledge base is to provide a clear and scalable structure to gather cyber security knowledge. This knowledge has multilple dimensions that relate to one another: 
- Processes and Methods:
	- there are multiple topics such as penetration testing and security engineering and secure operations
	- they are generally technology-agnostic and provide the principles and techniques to apply. Rather the what, not the how.  
	- Note: For now, only pentesting methods are fully integrated into the knowledge base.
-  Technologies and tech-specific procedures: 
	-  each of the topics above, and their sub-topics create a distinct perspective on a technology
	- eg. the http protocol can be used for enumeration, as well as exploitation but it can also be hardened and operated securely
- Tools:
	- The security world is filled with a plethora of tools that serve one or many purposes.

The goal of security-notes is to present each of these dimensions in a coherent manner, but at the same time model their interconnections in a clear and low-effort way.

This leads to the following structure and formatting rules.
# Knowledge Base Structure
## Directory Structure
On a top level, the above mentioned dimensions are represented as top level folders which are then detailed and further splitted in subfolders:
- /Methods
	- /Pentesting
	- /Security-Engineering
- /Tech-Specifics
	- /Web
	- /Cloud
	- /Network
	- /OS
	- /ICS
- /Tools
	- /Pentesting
	- Engineering
## Notes Structure
### Structure of Pentesting Method Notes
Pentesting Methods are structured followring the MITRE ATT@CK Framework. Specifically, the Tactics of the "Enterprise Matrix" are used.
### Structure of Tech-Specifics Notes
Technology notes use the following overall structure:
- Fundamentals
- Pentesting
	- Provides useful information how to pentest the technology.
	- A subsection for each tactic can be created.
- Hardening
Technology Notes can be splittet into multiple notes - e.g. making a "pentesting" folder for web technologies where then each technique is a seperate note.
### Structure of Tool Notes
Each tool note shall provide the most important knowledge and potential tipps/tricks and useful commands to copy/paste.
The goal is NOT to provide a complete guide or reference for a tool - these shall be provided by external links.
Tool notes can contain sections about how the tool can be used to test a specific technology - this section can then be embedded in a technology note.
## How it all comes together
### Integration of Technologies and Pentesting Methods
For each technology (and possibly tool), tags are set to identify the MITRE ATT@CK Enterprise tactics they are relevant for. Based on that, queries can be used in method notes to identify all technologies that can be (ab)used for a specific tactic. Further, simple links can be used.

**Tags:**
- In
	- #tactic/reconnaissance
	- #tactic/ressource-development
	- #tactic/initial-access
	- #tactic/execution
- Through
	- #tactic/persistence
	- #tactic/privilege-escalation
	- #tactic/defense-evasion
	- #tactic/credential-access
	- #tactic/discovery
	- #tactic/lateral-movement
- Out
	- #tactic/collection
	- #tactic/command-and-control
	- #tactic/exfiltration
	- #tactic/impact
### Integration of Tools and Technologies
Each tool that is useful to pentest or audit a certain technology is linked from the respective technology note.

A query can then be used to provide an overview of the technologies the tool relates to.
e.g. nmap is useful for a variaty of technologies, while snmp-walk is specific to the snmp protocol.
# Comparison to HackTricks Wiki
The HackTricks Wiki consists of [HackTricks](https://book.hacktricks.wiki/en/index.html)  and [HackTricks Cloud](https://cloud.hacktricks.wiki/en/index.html). Combined  they are a vast knowledge base that goes into detail that this knowledge base does not provide for most topics.  However, my security-notes knowledge base focuses more on providing a "walkthrough" for usual pentesting screnarios. That means  that  means, that  a bigger focus is put on the techniques including when and how to use them in a structured pentest. HackTricks can then be used as a Wiki to extract detailed information about certain details. 