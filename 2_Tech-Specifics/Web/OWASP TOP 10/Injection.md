**Type:** #type/theory
**Tags:** #goal/exploitation 

---

data entered by the user is not filtered or validated
-> the user can enter - "inject" commands/code/queries into the system

multiple scenarios are possible:
- [[2_Tech-Specifics/Web/Web Application Attacks/Command Injection|command injection]]: inject os/shell commands
- hibernate injecition: java database stuff
- LDAP injection: inject stuff into the domain
- HTML
- Javascript
- XML
- [[2_Tech-Specifics/Web/Web Application Attacks/SQL Injection|SQL injection]]

### Impact:
- data loss
- data manipulation
- sensitive data disclosure
- combined with other vulnerabilites -> root access to server

### Defence:
- allow list: only allow input that is registered in a list of save inputs
- input stripping/black listing: remove dangerous characters from input (dont rely only on this -> better is whitelisting)
- use paremeterized queries to seperate commands from data
- limit number of characters in the queries