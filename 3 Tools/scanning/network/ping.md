**Tags:** #type/tool #tactic/reconnaissance/active #tactic/discovery
**Link:** 
**Purpose:** test if host is up

---
# Info
- uses ICMP echo requests
# Usage
- you can specify th number of requests to be sent ( on linux: `-c`, on windows `-n`)
- ping until the host respnds: `-t`
## reasons for ping not beeing successul
- firewalls might block ICMP requests
- target is not connected to network
- you are not connected to network 