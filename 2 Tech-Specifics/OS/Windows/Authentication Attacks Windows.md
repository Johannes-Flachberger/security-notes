---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

See [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows|Fundamentals - Windows]]

# Pentesting

## Local Credential Access

Extract password hashes from local [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Hash Sources|Hash Sources]].

**Prerquisites:**

- Administrator privileges
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

Tools:

- [[3 Tools/mimikatz|mimikatz]]
- [built-in tools to dump LSASS memory](https://blog.cyberadvisors.com/technical-blog/attacks-defenses-dumping-lsass-no-mimikatz/)

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
- [pth-tooklit](https://github.com/byt3bl33d3r/pth-toolkit): binaries for various protocols
- Many other tool support pass the hash

## NTLMv2 Response Cracking

During the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#NTLMv2|NTLMv2 handshake]], the client response can be captured and the included hash can be cracked to obtain the cleartext password.

The response has the following format: `username::domain:server_challenge:client_response:blob`

**Workflow:**

1. Capture a client response - e.g. by:
	- sniffing, e.g. using [[3 Tools/passive recon/Wireshark|Wireshark]]
	- set up an smb server (e.g. using [[3 Tools/network/Responder|Responder]]) and trigger the target to perform and smb request to this server - e.g. see [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#UNC Paths|UNC Paths]]
- Crack the included "Net-NTLMv2 hash" - see [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]]

## NTLMv2 Relay Attack

If you can capture an NTLMv2 client response but cannot crack it - you can relay the authentication request to a legitimate server to execute commands on it.

**Prerequisites:**

- (Unprivileged) access to a windows client.
- User whose request is relayed must be a local admin or UAC must be turned off on the server

**Workflow:**

1. Set up a tool to relay the requests
2. from the windows client, send a request (e.g. SMB or HTTP) to the relay tool

**Tools:**
- [[3 Tools/network/impacket-scripts#Impacket-ntlmrelayx|Impacket-ntlmrelayx]]

# Hardening

- disable, or limit the use of NTLM as far as possible
