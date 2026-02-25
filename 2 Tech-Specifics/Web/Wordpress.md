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

**Tools:**
- wpscan: very useful
	- e.g. `wpscan --url <url> --enumerate p --plugins-detection aggressive -o <output file>`
	- can scan for vulnerabilities if API token is given (requires free registration)
	- see: <https://www.kali.org/tools/wpscan/>

## Privilege Escalation

Once you have admin access to the wordpress management console, you can add a webshell or reverse shell as a wordpress plugin.

- Plugins are basically zipped .php files
- Useful ressources:
	- <https://github.com/jckhmr/simpletools/tree/master/wonderfulwebshell>
	- <https://jckhmr.net/create-a-wordpress-webshell-plugin/>
	- <https://github.com/amtzespinosa/wp-backdoor?tab=readme-ov-file>

# Hardening
