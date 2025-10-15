tags: #type/theory #tech/protocol

---
# Email - SMTP-POP-IMAP
**everything is sent in cleartext!**  
however, often TLS (transport layer security) is added: [[2_Tech-Specifics/Network/Protocols/SMTPS,POP3S,IMAPS|SMTPS,POP3S,IMAPS]]
## SMTP

## POP3
- default port 110
- used to download emails  from Mail delivery agent (MDA)
- cannot synchronize over multiple clients
- credentials are send in cleartext
## IMAP
- makes it possible to keep your email synchronized across multiple devices (and mail clients)
- default port 143
- credentials are sent in cleartext
