**Type:** #type/tool
**Tags:**  #tactic/reconnaissance/passive 
**Link:** https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nslookup
**Purpose:** perform dns lookups

---
# Info
available per default on windows 
can do dns lookups for IPv4, IPv6, Mailservers,...
# Usage

`nslookup OPTIONS DOMAIN_NAME SERVER`
SERVER = DNS Server, eg. `1.1.1.1.`, `8.8.8.8`
define query type in options `-type=[TYPE]`
