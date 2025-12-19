---
tags:
  - "#type/tech-specific"
---
# Fundamentals
Antivirus vs. EDR: EDR solutions additionally share data with a SIEM, to enable further analysis. 

Detection can be based on multiple types of artefacts:
- Files
	- Disassembled binaries: Supports cracking obfuscation by finding en/decoding routines,...
- Memory
- Network
- Events in specific applications, e.g. the Web Browser
- Emulation in a Sandbox
	- Supports detecting of obfuscated malware
## Detection Methods
Modern products rely on multiple detection methods:
**Signature based**
- e.g. using [YARA Rules](https://en.wikipedia.org/wiki/YARA)
- can detect known threats
**Heuristic based**
- search for different kinds of pattern
- often based on disassembled binaries
**Behaviour Based Detection**
- execute the file in a sandbox and monitor the actions 
**Machine Learning based**
- can detect unknown malware, or variations of known malware
- based on samples and metadata 


# Pentesting
[[3 Tools/Malware analysis/VirusTotal|VirusTotal]]

# Hardening
