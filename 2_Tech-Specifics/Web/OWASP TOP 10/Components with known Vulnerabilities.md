**Type:** #type/theory
**Tags:**  #goal/exploitation 

---

- it is not clear which components/libraries/dependencies are used
- used components are not checked against CVE databases

### Impact
Libraries which are used a lot are often attacked & automated exploits often  exist
### Defense:
- remove all unused libraries
- regularly check libraries/for vulnerabilites e.g. with [[3_Tools/web/OWASP dependency checker]]
Check for the software component versions and check for known vulnerabilities
