---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
---
# Fundamentals

If you can capture an NTLMv2 client response but cannot crack it - you can relay the authentication request to a legitimate server to achieve command execution on it.

# Pentesting

**Prerequisites:**

- (Unprivileged) access to a windows client.
- User whose request is relayed must be a local admin or UAC must be turned off on the server

**Workflow:**

1. Set up a tool to relay the requests
2. from the windows client, send a request (e.g. SMB or HTTP) to the relay tool

**Tools:**
- [[3 Tools/network/impacket-scripts#Impacket-ntlmrelayx|Impacket-ntlmrelayx]]

# Hardening
