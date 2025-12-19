Welcome to my personal cyber security knowledge base. I collect know-how from many different sources and try to summarize it here in a structured way. Of course, this will never be complete or perfect, so its always work in progress. Have Fun :)
# Usage
This is an [obsidian](https://obsidian.md/) vault. Clone the repo and open it in obsidian.

# Philosophy
The goal of this knowledge base is to provide a clear and scalable structure to gather cyber security know-how. This know-how has multiple "dimensions" that relate to one another:
- **Methods:**
	- methods are technology-agnostic
	- they provide principles and guidance
	- e.g. penetration testing processes, reconnaissance checklists,...
-  **Technologies and their specifics:** 
	- technologies often have distinct ways to attack & and harden them
	- eg. web-apps have other attack vectors than an operating system
- **Tools:**
	- a plethora of security-related tools exist
	- each tool can be used for one specific or lots of different purposes

The goal of security-notes is to present each of these dimensions in a coherent manner, but at the same time model their interconnections in a clear and low-effort way.

This leads to the following structure and formatting rules.
# Knowledge Base Structure
## Directory Structure
The above mentioned dimensions are represented as top level folders which are further split in more specific topics:
- /Methods  
	- /Security-Engineering  
	- /Pentesting  
		- /0 Preparation  
		- /1 Reconnaissance  
		- etc.  
- /Tech-Specifics  
	- /Web  
	- /Cloud  
	- /Network  
	- /OS  
	- /ICS  
	- etc.  
- /Tools  
	- /exploitation-frameworks  
	- /scanning  
## Notes Structure
According to the folder structure, templates are used for different types of notes.
### Structure of Tech-Specific Notes
The following sections are used in each tech-specific note:  
- Fundamentals  
- Pentesting  
	- Provides useful information how to test the technology.  
	- Structured based on MITRE ATT@CK tactics  
- Hardening  
Tech-specifics can be split into multiple notes - e.g. making a "pentesting" folder for web technologies which holds attack vectors as separate notes.
### Structure of Tool Notes
Each tool note provides the most important information, tipps/tricks and useful snippets to copy/paste.  
The goal is NOT to provide a complete guide or reference for a tool - these are provided as external links.  
Tool notes can contain sections about how the tool can be used to test a specific technology - this section can then be referenced by a technology note.
## How it all comes together
### Interconnection of Methods with Tech-Specific and Tool Notes 
For each technology and tool, tags are set to identify the [MITRE ATT@CK Enterprise tactics](https://attack.mitre.org/tactics/enterprise/) they are relevant for. Based on that, queries are used in method notes to identify all technologies that can are related to a specific tactic. 

**Allowed Tags:**
- attack/reconnaissance
- attack/ressource-development
- attack/initial-access
- attack/execution
- attack/persistence
- attack/privilege-escalation
- attack/defense-evasion
- attack/credential-access
- attack/discovery
- attack/lateral-movement
- attack/collection
- attack/command-and-control
- attack/exfiltration
- attack/impact
### Interconnection of Tools and Tech-Specifics
Tools are referenced in tech-specific notes, were they are useful.
# Comparison to HackTricks Wiki
The HackTricks Wiki consists of [HackTricks](https://book.hacktricks.wiki/en/index.html)  and [HackTricks Cloud](https://cloud.hacktricks.wiki/en/index.html). Combined  they provide a vast knowledge base that goes into detail that this knowledge base currently cannot provide.

However, whis security-notes knowledge base focuses more on providing a "walkthrough", containing the most important content in condensed form. HackTricks can then be used as a Wiki to further reading where required.