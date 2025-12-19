---
tags:
  - "#type/tech-specific" 
  - "#attack/reconnaissance/active" 
  - "#attack/privilege-escalation"
---
# Fundamentals
Popular web application framework
# Pentesting

## Enumeration
A very useful tool is "wpscan" - see: https://www.kali.org/tools/wpscan/
## Privilege escalation
Once you have admin access to the wordpress management console, you can add a webshell or reverse shell as a wordpress plugin.
- Plugins are basically zipped .php files
- Useful ressources:
	- https://github.com/jckhmr/simpletools/tree/master/wonderfulwebshell
	- https://jckhmr.net/create-a-wordpress-webshell-plugin/
	- https://github.com/amtzespinosa/wp-backdoor?tab=readme-ov-file
# Hardening
