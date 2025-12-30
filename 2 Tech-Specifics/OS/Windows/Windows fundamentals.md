---
tags:
  - "#type/tech-specific" 
---
# Built-in Tools

- **Run things**
	- use the `run` dialog
- **computer management**
	- utility: `compmgmt.msc`
	- access all the important utilities for managing the system.
- **User and Group management**
	- run `lusrmgr.msc`
- **System Configuration**
	- utility: `msconfig`
	- local admin rights needed
- **task manager**
	- utility: `taskmgr`

# Accounts & Privilege Levels

- **Administrator (local):** This is the user with the most privileges.
- **Standard (local):** These users can access the computer but can only perform limited tasks. Typically these users can not make permanent or essential changes to the system.
- **Guest:** This account gives access to the system but is not defined as a user.
- **Standard (domain):** Active Directory allows organizations to manage user accounts. A standard domain account may have local administrator privileges.
- **Administrator (domain):** Could be considered as the most privileged user. It can edit, create, and delete other users throughout the organization's domain.
- **SYSTEM account:** you cant log in, but it is used by services installed on the machine

# Authentication Protocols

## NTLMv1

Challenge - response based authentication protocol. Uses the NT hash as long-term secret. It is prone to multiple attacks, such as:

- [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]]
- replay
- spoofing, etc.

## NTLMv2

Improvement of NTLMv1. Adds a client challenge to prevent server spoofing. Also has protection against replay attacks. [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]] is still possible.

## Kerberos

#todo

# UNC Paths

See: [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/standard/io/file-path-formats#unc-paths)

Universal naming convention (UNC) paths are used to access network ressources using [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]]. They can be used and exploited at many different places. E.g.:

- [[2 Tech-Specifics/OS/Windows/cmd|cmd]]
- [[2 Tech-Specifics/Web/WebApp Attacks/Web Upload Vulnerabilities|Web Upload Vulnerabilities]]
- [[2 Tech-Specifics/Web/WebApp Attacks/Directory Traversal|Directory Traversal]]

Further reading: [https://www.netspi.com/blog/technical-blog/network-pentesting/10-places-to-stick-your-unc-path/](https://www.netspi.com/blog/technical-blog/network-pentesting/10-places-to-stick-your-unc-path/)
