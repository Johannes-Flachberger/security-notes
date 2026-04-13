---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

Kerberos

**Defaults Ports:**

- tcp88
- udp88

Stateless protocol, Ticket-Based authentication.

3 Main Entities:

- Principal (client in Kerberos Terms)
- Ressource/Application/Service: the entity the principal wants to access
- The Key Distribution Center (KDC) issues access keys to clients. The KDC service often runs on the Domain controller.

Detailed explanations:

- [WikiPedia](https://en.wikipedia.org/wiki/Kerberos_(protocol))
- [HackTheBox](https://www.hackthebox.com/blog/what-is-kerberos-authentication)

## Authentication Steps

**Pre-authentication (e.g. when logging in to a machine):**

1. Client sends _Authentication Server Request_ (AS-REQ) to Authentication Server (often the Domain Controller)
	- AS-REQ contains a timestamp encrypted with the clients password hash
		- If pre-auhtentication is disabled, anyone can send an AS-REQ (without credentials)
2. Authentication Server sends _Authentication Server Reply (AS-REP)_
	- it contains:
		- a TGS session key: encrypted with the users password hash
		- a ticket-granting ticket (TGT): encrypted with the NTLM hash of the [_krbtgt_](https://adsecurity.org/?p=483) account
		- TGTs are valid for 10 hours per default

**Before accessing a service:**

3. Client creates a _Ticket Granting Service Request_ (TGS-REQ) and sends it to the KDC
4. KDC replies with the _Ticket Granting Service Reply_ (TGS-REP)
	- it contains:
		- name of the service the ticket is granted to
		- session key for authentication to a service
		- a "Ticket Granting Service" (TGS) (also called service ticket) with username & group information of the client: encrypted with the service's [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|NTLM hash]]
	- **Note:** The KDC does NOT check, if the client is allowed to access the application it requests a ticket for. This is the applications responsibility. --> A TGS is always granted.

**Authentication to a service:**

5. Client sends _Application Request_ (AP-REQ) to the service it wants to connect to (e.g. a webserver, smb share, etc. )
	- The AP-REQ contains the TGS encrypted with the service users NTLM hash
6. Service decides if the client has access, based on the information included in the TGS

**Note:** TGTs and Service Tickets are cached by LSASS on client machines for further use. --> It might be possible to extract them with [[3 Tools/mimikatz|mimikatz]].

> [!Hint] Capabilities of TGT & TGS
> - A TGT is bound to the host it was issued for, but can be used to authenticate against any SPN in the network.
> - A TGS is bound to the SPN of the target service, but is NOT bound to a specific client / host. --> It can be exported and reused from another client - see [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/Pass the Ticket|Pass the Ticket]]

# Pentesting

## Credential Access

### Brute Force / Dictionary

AS-REQ queries can be used against a domain controller to check if a set of credentials is valid.

**Tools:**

- [[3 Tools/bruteforce/netexec|netexec]]: multiple protocols possible, best use ldap
- [[3 Tools/microsoft/Kerbrute|Kerbrute]]: from windows

**See also:**

- [[2 Tech-Specifics/Active Directory/Credential Access - AD/Password Attacks - AD Specifics|Password Attacks - AD Specifics]]
- [[1 Methods/Security-Testing/3 Initial Access/Password Attacks|Password Attacks]]

### AS-REP Roasting

**Goal:** Obtain a TGT for an arbitrary domain user and attempt a brute-force attack on the user.

**Prerequisite:** Kerberos Pre-Authentication must be disabled. This can be done per-user with the option "Do not require Kerberos preauthentication". By default, pre-authentication is enabled.

If pre-authentication is disabled, anyone knowing a valid username (e.g. from [[2 Tech-Specifics/Active Directory/Enumeration - AD/Overview - Enumeration - AD|Enumeration]]) can make an AS-REQ for the target user and receive a TGT. Since the TGT is encrypted with the password hash of the user, the password can be [[1 Methods/Security-Testing/3 Initial Access/Password Attacks#Local Attacks (Hash-cracking)|brute-forced locally]], e.g. using [[3 Tools/crypto/Hashcat|Hashcat]] (search modes for "Kerberos").

**Note:** The brute-forcing involves first creating the hash of a candidate password and then trying to decrypt the TGT. If the result is a valid TGT, the password was right.

**Tools:**

- [[3 Tools/network/impacket-scripts#Impacket-GetNPUsers|impacket-GetNPUsers]]
	- used from kali
	- uses valid credentials to automatically identify vulnerable users and get TGTs for them
- [[3 Tools/microsoft/Rubeus|Rubeus]]
	- used from windows, when having a session with a domain user
	- searches for AS-REP roastable users automatically and roasts them

**Further Reading:** [Medium](https://harmj0y.medium.com/roasting-as-reps-e6179a65216b)

#### Targeted AS-REP Roasting

If you "Do not require Kerberos preauthentication" is disabled, but you have the necessary [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Object permissions|Permissions]] on a user, you can activate the privilege and then carry out AS-REP roasting on the user.

### Kerberoasting

**Goal:** Obtain a service ticket for any service within the domain and attempt a brute-force attack on the service accounts password.

Two characteristics make Kerberoasting relevant:

- When a client requests a TGS for a specific service (identified by an [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Service Principal Names (SPN)|SPN]]), the KDC does not check if the client is allowed to access the application. --> A TGS can be requested for any application within the domain.
- The service ticket / ticket-granting-service is encrypted with the service user's hash.

--> Any client having a TGT can make a TGS-REQ for any service on the domain and will receive the corresponding TGS-REP. The TGS-REP can be [[1 Methods/Security-Testing/3 Initial Access/Password Attacks#Local Attacks (Hash-cracking)|brute-forced locally]], to extract the service users password e.g. using [[3 Tools/crypto/Hashcat|Hashcat]] (search modes for "Kerberos").

**Note:** The brute-forcing involves first creating the hash of a candidate password and then trying to decrypt the service ticket. If the result is a valid service ticket, the password was right.

**Tools:**

- [[3 Tools/microsoft/Rubeus|Rubeus]]
	- used from windows
	- automatically searches for SPNs and Kerberoasts them
- [[3 Tools/network/impacket-scripts#Impacket-GetUserSPNs|impacket-GetNPUserSPNs]]
	- used from kali
	- uses valid credentials to automatically identify vulnerable users and get TGTs for them

**Further Reading:** [harmj0y.net](https://blog.harmj0y.net/redteaming/kerberoasting-revisited/)

> [!Hint] Kerberosting managed service accounts
> Computer accounts, [managed service accounts](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/managed-service-accounts-understanding-implementing-best/ba-p/397009), and [group-managed service accounts](https://docs.microsoft.com/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview), typically have randomly-generated 120 character long passwords.
> - --> Kerberoasting is not feasable for managed users, including `krbtgt`
> - --> Kerberoasting is feasable for services running as user accounts.

#### Targeted Kerberoasting

If you have the necessary [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Object permissions|Permissions]] on a user, you can set an [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Service Principal Names (SPN)|SPN]] for the user then carry out Kerberoasting on the user. This creates less friction than e.g. changing the users password.

### Forging Tickets

#### Silver Tickets

If you have the password or NTLM hash of a service account, you can forge a service-ticket with **arbitrary permissions** and an **arbitrary client user** for the service - this is called a "Silver Ticket".

**Prerequisite:**

- Access to the Password, or NTLM hash of the targeted service account.
- Local admin (for [[3 Tools/mimikatz|mimikatz]])

**Workflow:**

1. Use [[3 Tools/mimikatz#Forging Kerberos Tickets|mimikatz]] to forge a silver ticket.
2. Connect to the service with the forged ticket
	1. e.g. using [[3 Tools/shells/PowerShell#Download a File|Invoke-WebRequest]] for webservices

### Golden Tickets

In the [[2 Tech-Specifics/Network/Protocols/Kerberos|Kerberos]] authentication flow, each TGT issued by the KDC is encrypted using the `krbtgt` users password hash. --> If you can somehow obtain the password hash, you can forge custom TGTs, granting the user any group memberships and permissions. It is not uncommon that the `krbtgt` password is only changed rarely and to find very old krbtgt passwords.

**Prerequisites:**

- access to the password hash of the `krbtgt` account
**Workflow:**
1. Use [[3 Tools/mimikatz#Golden Tickets|mimikatz]] to forge a golden ticket.
2. Use the TGT to connect to any resource on the domain - see [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/Overview - Lateral Movement - AD|Active Directory Lateral Movement]]

**Note:** Once the password hash is obtained TGTs can be created at ANY machine (also non-domain joined machines)

# Hardening

Configure services to always perform PAC validation against the domain controller before authenticating a user.
