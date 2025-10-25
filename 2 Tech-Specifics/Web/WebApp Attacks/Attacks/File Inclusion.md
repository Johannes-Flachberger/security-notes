**Tags:** #type/tech-specific #tactic/execution #tactic/credential-access #tactic/exfiltration #tactic/discovery 

---
# Fundamentals
allows to include the contents of a file in the webapp code --> possible code execution or file display, similar to [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Directory Traversal|Directory Traversal]]
## Local File Inclusion (LFI)
- exploits the include function (used eg. used to include javascript in a php file)
## Remote File Inclusion (RFI)
- option `allow_url_fopen` on the webserver needs to be set

# Pentesting
- can be combined with [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Upload vulnerabilities|Upload vulnerabilities]], or [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Injection Attacks/Logfile Poisoning|Logfile Poisoning]] to achieve code execution
- error messages help a lot to figure out how the webserver is accessing the files
- [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]] can provide useful information

# Hardening


