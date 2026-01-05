---
tags:
  - "#type/tool" 
  - "#attack/reconnaissance/active" 
  - "#attack/discovery"
Link: 
Purpose: test if host is up
---
# Info

- uses ICMP echo requests

# Usage

- you can specify th number of requests to be sent ( on linux: `-c`, on windows `-n`)
- ping until the host respnds: `-t`

## Reasons for Ping not Beeing Successul

- firewalls might block ICMP requests
- target is not connected to network
- you are not connected to network
