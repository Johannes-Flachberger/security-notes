---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

Extract password hashes or tickets from local [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Local Credential Sources|Hash Sources]].

# Pentesting

**Prerquisites:**

- Administrator privileges
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

**Tools:**

- [[3 Tools/mimikatz|mimikatz]]
- [built-in tools to dump LSASS memory](https://blog.cyberadvisors.com/technical-blog/attacks-defenses-dumping-lsass-no-mimikatz/)

# Hardening

disable, or limit the use of NTLM as far as possible
