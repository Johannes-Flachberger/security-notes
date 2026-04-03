---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

During the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#NTLMv2|NTLMv2 handshake]], the client response can be captured and the included hash can be cracked or relayed.

# Pentesting

The NTLMv2 response has the following format: `username::domain:server_challenge:client_response:blob`

The client response includes the "Net-NTLMv2 hash".

**Workflow:**

1. Capture a client response - e.g. by:
	- sniffing, e.g. using [[3 Tools/passive recon/Wireshark|Wireshark]] or
	- set up an smb server (e.g. using [[3 Tools/network/Responder|Responder]]) and trigger the target to perform and smb request to this server - e.g. inject a [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#UNC Paths|UNC Path]]
2. Use the hash for further attacks - e.g:
	- Crack the hash - see [[1 Methods/Security-Testing/3 Initial Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]]
	- Relay the handshake: [[2 Tech-Specifics/OS/Windows/Lateral Movement - Windows/NTLMv2 Relay Attack|NTLMv2 Relay Attack]]
	- Create a Kerberos TGT: [[2 Tech-Specifics/Active Directory/Credential Access - AD/Overpass the Hash|Overpass the Hash]]

# Hardening

disable, or limit the use of NTLM as far as possible
