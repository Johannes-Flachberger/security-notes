---
tags:
  - "#type/tool" 
  - "#attack/reconnaissance/passive" 
Link: https://linux.die.net/man/1/dig
Purpose: perfom DNS lookups 
---
# Info

DNS fundamentals: [[2 Tech-Specifics/Network/Protocols/TCP,UDP 53 DNS|TCP,UDP 53 DNS]]

alternative tool: `host` command in kali

# Usage

`dig [@SERVER] <DOMAIN_NAME> <TYPE>`

| Option        | Command                  |
| ------------- | ------------------------ |
| `TYPE`        | DNS record type to quers |
| `DOMAIN_NAME` | domain                   |
| `SERVER`      | DNS server to use        |
