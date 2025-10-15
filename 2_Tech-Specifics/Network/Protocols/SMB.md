**Type:** #type/theory
**Tags:** #tech/protocol #tactic/reconnaissance/active 

---
# Theory
Server Message Block
SMB often goes along with netbios, which was historically used for computers to communicate with each other
SMB default port: 445
netbios default port: 139
for manipulating remote data
# Pentesting
## Enumeration
### Nmap:
![[3_Tools/scanning/network/nmap snippets#^90d962|nmap snippets]]
## nbtscan
e.g. `sudo nbtscan -r 192.168.50.0/24`
`-r` sets originating udp port to 137
# Tool collection
[[3_Tools/network/SMB tools|SMB tools]]
