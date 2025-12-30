---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals
Windows uses NTLM hashes - also see [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|Hashing fundamentals]]
**Hash sources:**
- Hashes are stored in the Security Account Manager (SAM) at `C:\Windows\system32\config\sam`. Several protections are applied on the database file.
- The Local Security Authority Subsystem (LSASS) is the windows process that handles everything related to authentication. Hashes of both local users and logged-in domain users can be extracted from its memory (privileges required!)
# Pentesting
## Local Credential Access
Tools:
- [[3 Tools/mimikatz|mimikatz]]
## Pass the Hash
Pass the hash abuses a fundamental design flow in NTLM authentication: in the NTLM challenge - response, the client responds with its (encrypted) hash to prove its authenticity. --> The cleartext password is not required, only the password hash.

Further reading: [Wikipedia](https://en.wikipedia.org/wiki/Pass_the_hash)

**Workflow:**
1. Harvest Hashes - see [[#Local Credential Access]]
2. Use the hash to authenticate to a remote service as the

**Tools:**
# Hardening
- disable, or limit the use of NTLM as far as possible