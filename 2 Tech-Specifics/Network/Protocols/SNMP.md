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

Data that is accessible by SNMP is organized in the "Management Information Base (MIB)". Each "datapoint" is identified by an OID, which contains an address and metadata. OIDs follow a tree structure. --> when enumerating you can start at the very root, or at a specific place. Some MIB branches are standardaized and therefore use the same OIDs accross manufacturers, but some are vendor specific.

The MIB holds a lot of information about targets - e.g. on windows: user accounts, running programs, etc...

# Pentesting

**Workflow:**

1. port scan
2. build list of community strings & brute force
3. [[#Enumeration|enumerate]] the MIB

## Enumeration

### Snmpwalk

- enumerates the MIB of an smb server, starting from the defined OID
	- per default, only the "mib-2-subtree" is enumerated, but the extended MIB can provide further information.
- requires credentials / community string
**Example:** `snmpwalk -c public -v1 -t 10 192.168.50.151 .1`

**E.g. - walk the extended MIB:** `snmpwalk -v 1 -c public <IP> NET-SNMP-EXTEND-MIB::nsExtendOutputFull`

| Option           | Purpose                                                                           |
| ---------------- | --------------------------------------------------------------------------------- |
| `-c`             | community string                                                                  |
| `-v`             | snmp version                                                                      |
| `-t`             | timeout                                                                           |
| `-Oa`            | decode hex strings to ascii                                                       |
| `<starting OID>` | the OID where to start walking the MIB tree - use `.1` to enumerate the whole MIB |

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
