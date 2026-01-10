---
tags:
  - "#type/tool"
  - "#attack/ressource-development"
Link: https://www.shellterproject.com/homepage/
Purpose: antivirus evasion (dynamic shellcode injection)
---
# Info

Best free antivirus evasion tool. Also has a paid version with advanced features.

Analysis a target PE/exe file and injects shellcode into the file.

**Free Version**
- Supports 32bit targets only.
- Good but limited evasion techniques

**Paid Version**
- Supports both 32bit and 64 bit targets.
- Advanced evasion techniques

On kali available at: `/usr/share/windows-resources/`

# Usage

Shellter is built for windows --> use wine on linux.

## Workflow

1. Choose a target executable.
2. Start Shellter

## Options

| Option           | Purpose                               |
| ---------------- | ------------------------------------- |
| `automatic mode` | guides you through the process        |
| `manual mode`    | gives low level, granular control     |
| `stealth mode`   | attempt to restore the execution flow |

# Snippets
