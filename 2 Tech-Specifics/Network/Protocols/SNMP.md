---
tags:
  - "#type/tech-specific"
  - "#type/tool"
  - "#attack/credential-access"
---
# Fundamentals

**Detailed Fundamentals:** [[2 Tech-Specifics/Network/Protocols/Fundamentals/SNMP Fundamentals|SNMP Fundamentals]]

**Default Ports:**

- udp161 for queries
- udp162 for traps

**Properties:**

- often not well understood by network engineers --> prone to misconfigurations
- based on UDP, stateless, simple --> prone to spoofing & replay
- SNMP 1,2 & 2c is unencrypted --> interception
- [[2 Tech-Specifics/Network/Protocols/Fundamentals/SNMP Fundamentals#4️. SNMP Versions|SNMPv3]] supports encryption, message integrity and authentication - old versions only supported DES-56, which can be brute forced

The MIB holds a lot of information about targets - e.g. on windows: user accounts, running programs, etc...

# Pentesting

## Workflow

1. port scan
2. build list of community strings & brute force
3. [[#Enumeration|enumerate]] the MIB

## Enumeration

### Snmpwalk

- enumerates the whole MIB tree of an smb server
- requires credentials / community string
e.g. `snmpwalk -c public -v1 -t 10 192.168.50.151`

| Option | Purpose |
|----------|--------------|
| `-c` | community string |
| `-v` | snmp version |
| `-t` | timeout |
| `-Oa` | decode hex strings to ascii |

## Snmp-check

- more readable/structured output than snmpwalk
- automated enumeration of MiB
- finishes enumeration before it provides an output --> needs some time
e.g. `snmp-check -c public 192.168.50.151`

## Credential Access

## Onesixtyone

- bruteforces a list of snmp agents using the provided wordlist
e.g. `onesixtyone -c community -i ips`

| Option | Purpose |
|----------|--------------|
| `-c` | list of community strings |
| `-i` | list of ips |
