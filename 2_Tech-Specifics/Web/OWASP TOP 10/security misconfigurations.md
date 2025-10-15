**Type:** #type/theory
**Tags:**  #goal/exploitation 

---

Security misconfigurations include:

-   Poorly configured permissions on various levels: OS, Network, services, webserver, databases
-   Having unnecessary features enabled, like services, pages, accounts, preinstalled software, open ports
-   Default accounts with unchanged passwords
-   Error messages that are overly detailed and allow an attacker to find out more about the system
-   Not using [HTTP security headers](https://owasp.org/www-project-secure-headers/), or revealing too much detail in the Server: HTTP header
- use of broken crypto

### Impact
- access to system
### Defense
- minimal necessary functionality
- use dev-ops to have defined security standards in production software
- error messages that do not disclose sensitive data