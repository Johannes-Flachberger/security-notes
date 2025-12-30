---
tags:
  - "#type/tool"
  - "#attack/credential-access"
  - "#attack/collection"
Link: https://www.kali.org/tools/responder/
Purpose: IPv6/IPv4 LLMNR/NBT-NS/mDNS Poisoner and NTLMv1/2 Relay.
---
# Info

supports many different protocols, such as http, smb, smtp,...

# Usage

E.g.: `sudo responder -I tun0`

| Option | Purpose                     |
| ------ | --------------------------- |
| `-I`   | specify interface to run on |

logs are written to `~/responder/logs`
