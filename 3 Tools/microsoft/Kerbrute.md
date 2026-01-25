---
tags:
  - "#type/tool"
  - "#attack/credential-access"
Link: https://github.com/ropnop/kerbrute
Purpose: dictionary attacks on kerberos
---
# Info

Uses AS-REQ queries to check if credentials are valid.

The following modes are supported:

- **bruteuser** - Bruteforce a single user's password from a wordlist
- **bruteforce** - Read username:password combos from a file or stdin and test them
- **passwordspray** - Test a single password against a list of users
- **userenum** - Enumerate valid domain usernames via Kerberos

# Usage

Example:

`.\kerbrute_windows_amd64.exe <mode> -d <domain> .\usernames.txt "<password>"`

**Note:** The usernames file must be ANSI encoded. (oddly a wrong encoding can lead to network errors)

# Snippets
