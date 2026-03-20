---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
---
# Fundamentals

Pass the hash abuses a fundamental design flaw in [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Authentication Protocols|NTLM authentication]]: in the NTLM challenge - response, the client responds with its (encrypted) hash to prove its authenticity. --> The cleartext password is not required, only the password hash.

# Pentesting

Further reading: [Wikipedia](https://en.wikipedia.org/wiki/Pass_the_hash)

**Workflow:**

1. Harvest Hashes - see [[2 Tech-Specifics/OS/Windows/Credential Access - Windows/Overview - Credential Access - Windows|Overview - Credential Access - Windows]]
2. Use the hash to authenticate to a remote service

**Tools:**

- [[3 Tools/network/impacket-scripts#Impacket-psexec|impacket-psexec]]
- [[3 Tools/network/impacket-scripts#Impacket-wmiexec|impacket-wmiexec]]
- [[3 Tools/network/smb/smbclient|smbclient]]
- [pth-tooklit](https://github.com/byt3bl33d3r/pth-toolkit): binaries for various protocols
- Many other tools support pass the hash

# Hardening
