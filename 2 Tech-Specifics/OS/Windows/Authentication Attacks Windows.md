---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

Windows uses NTLM hashes - also see [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|Hashing fundamentals]]

## Hash Sources

- Hashes are stored in the Security Account Manager (SAM) at `C:\Windows\system32\config\sam`. Several protections are applied on the database file.
- The Local Security Authority Subsystem (LSASS) is the windows process that handles everything related to authentication. Hashes of both local users and logged-in domain users can be extracted from its memory (privileges required!)

# Pentesting

## Local Credential Access

Extract password hashes from local [[#Hash Sources]]. **Requires Administrator privileges.**

Tools:

- [[3 Tools/mimikatz|mimikatz]]

## Pass the Hash

Pass the hash abuses a fundamental design flow in NTLM authentication: in the NTLM challenge - response, the client responds with its (encrypted) hash to prove its authenticity. --> The cleartext password is not required, only the password hash.

Further reading: [Wikipedia](https://en.wikipedia.org/wiki/Pass_the_hash)

**Workflow:**

1. Harvest Hashes - see [[#Local Credential Access]]
2. Use the hash to authenticate to a remote service

**Tools:**

- [[3 Tools/network/impacket-scripts#Impacket-psexec|impacket-psexec]]
- [[3 Tools/network/impacket-scripts#Impacket-wmiexec|impacket-wmiexec]]
- [[3 Tools/network/smbclient|smbclient]]

## NTLMv2 Response Cracking

During the [[2 Tech-Specifics/OS/Windows/Windows fundamentals#NTLMv2|NTLMv2 handshake]], the client response can be captured and the included hash can be cracked to obtain the cleartext password.

The response has the following format: `username::domain:server_challenge:client_response:blob`

**Workflow:**

1. Capture a client response - e.g. by:
	- sniffing, e.g. using [[3 Tools/passive recon/Wireshark|Wireshark]]
	- set up an smb server (e.g. using [[3 Tools/network/Responder|Responder]]) and trigger the target to perform and smb request to this server - see [[2 Tech-Specifics/OS/Windows/Windows fundamentals#UNC Paths|UNC Paths]]
- Crack the included "Net-NTLMv2 hash" - see [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]]

# Hardening

- disable, or limit the use of NTLM as far as possible
