**Type:** #type/theory
**Tags:** #tactic/reconnaissance/active #tech/protocol 

---
# Fundamentals
- SMTP(simple mail transfer protocol): directs email to receiving mailbox
- everything is sent in cleartext
- Nice article about SMTP fundamentals: [https://computer.howstuffworks.com/e-mail-messaging/email3.htm](https://computer.howstuffworks.com/e-mail-messaging/email3.htm) 
- create a manual SMTP Session: https://www.atmail.com/blog/smtp-101-manual-smtp-sessions/
- Secure variant: SMTPS
# Pentesting
## Enumeration
Usernames can be enumerated using VRFY and EXPN commands
- VRFY: asks server if email address exists
- EXPN: asks server if user is part of a mailing list
Be careful to check what the response code actually means:
	Response Codes & Further commands: https://mailtrap.io/blog/smtp-commands-and-responses/
### Manual Enumeration
connect to port 25 and send commands manually
- Manual Connection with [[3_Tools/shells/Netcat#Manual SMTP Connection|Netcat]]
- Manual Connection with [[2_Tech-Specifics/Network/Protocols/Telnet|Telnet]]
### Automated enumeration
- [[3_Tools/Metasploit framework/Metasploit|Metasploit]]
	- Module `Smtp_version` - for getting information about the smtp server
	- Module `Smtp_enum` - for bruteforcing passwords