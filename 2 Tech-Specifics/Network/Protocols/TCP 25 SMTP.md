**Tags:** #type/tech-specific #tactic/reconnaissance/active 

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
Be careful to check what the response code actually means, dont rely just on the message the server sends: [Response Codes](https://mailtrap.io/blog/smtp-commands-and-responses/#SMTP-response-codes)
### Manual Enumeration
connect to port 25 and send [commands](https://mailtrap.io/blog/smtp-commands-and-responses/#Essential-SMTP-commands-in-the-order-they-may-be-used) manually
- Manual Connection with [[2 Tech-Specifics/Network/Protocols/TCP 23 Telnet|TCP 23 Telnet]]
- Manual Connection with [[3 Tools/shells/Socat|Socat]]
- Manual Connection with [[3 Tools/shells/Netcat#Manual SMTP Connection|Netcat]]
	- Note: sometimes, netcat does not send CRLF sequences, therefore better use telnet or socat
### Automated enumeration
- [[3 Tools/exploitation_frameworks/Metasploit/Overview - Metasploit|Overview - Metasploit]]
	- Module `smtp_version` - for getting information about the smtp server
	- Module `smtp_enum` - for bruteforcing passwords