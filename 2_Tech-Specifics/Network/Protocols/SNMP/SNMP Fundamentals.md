**Type:** #type/theory
**Tags:** #tech/protocol 

---
**Ports:**
- UDP 161 for queries
- 162 for traps

# Fundamentals
## 1️. What SNMP is

**SNMP** = **Simple Network Management Protocol**.  
It’s used to **monitor** and sometimes **control** devices on a network — routers, switches, servers, printers, UPS systems, etc.  
Think of it as a standardized way for one system (**the manager**) to ask another system (**the agent**) about its status or tell it to change something.

It can:
- Monitor health → CPU, memory, disk, temperature, fan speeds.
- Track network usage → Bytes in/out on interfaces.
- Detect failures → Link down traps, power issues.
- Remote control (carefully!) → Enable/disable ports, restart services.
- Inventory → Query device model, firmware version, serial number.
## 2️. Components
1. **Manager** — runs on your monitoring server (e.g., Zabbix, PRTG, Nagios).
2. **Agent** — runs on the device you want to monitor (Cisco IOS, Linux snmpd, etc.).
3. **MIB** (Management Information Base) — a “dictionary” of data points the device supports, each with an **OID** (Object Identifier).
	- tree structure, leaves hold values
	- very detailed ressource: https://www.ibm.com/docs/en/aix/7.1.0?topic=management-information-base
4. **Protocol** — SNMP over **UDP** (**default ports:** **161** for queries, **162** for traps).
## 3️. Common operations
- **GET** → Ask the device for a value (e.g., CPU usage, temperature).
- **GETNEXT** → Browse the MIB table one OID at a time.
- **GETBULK** → Get a chunk of OIDs at once (SNMPv2+).
- **SET** → Change a value (e.g., reboot a port, update config — if allowed).
- **TRAP / INFORM** → Device sends an _unsolicited_ event to the manager (e.g., “Port down!”).
## 4️. SNMP Versions
- **v1** — Old, cleartext, barely used now.
- **v2c** — Adds bulk requests, still cleartext (community strings as passwords).
- **v3** — Adds authentication & encryption (HMAC-MD5/SHA, DES/AES).
