---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

Extract password hashes or tickets from local [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Local Credential Sources|Hash Sources]].

# Pentesting

## Dump credentials from default hash sources

Extract password hashes or tickets from local [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Local Credential Sources|Hash Sources]].

**Prerquisites:**

- Administrator privileges
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

**Tools:**

- [[3 Tools/mimikatz|mimikatz]]
- [built-in tools to dump LSASS memory](https://blog.cyberadvisors.com/technical-blog/attacks-defenses-dumping-lsass-no-mimikatz/)

## Look for hashes or credentials at alternative locations

- [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
- **SAM and SYSTEM files in backups** - usually located at `C:\Windows\System32\` or `C:\Windows\System32\config` or `C:\Windows\System32\config\RegBack\`
- **configuration files** of installed software: (weak) configurations, credentials
- **.txt files**: credentials, spontaneous notes of users
- **password safe databases**
- relevant filetypes: `*.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx,*.ini, *.kdbx, *.kdb` etc.

# Hardening

disable, or limit the use of NTLM as far as possible
