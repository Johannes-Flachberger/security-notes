**Tags:** #type/tech-specific

---
# Vulnerability
sensitive data, such as credentials, ip adresses,... are exposed in requests, URLs,...
- data transfer over unencrypted protocols
- data is stored unencrypted (e.g. in sqLite database - things can be read by anybody)
- use of weak cryptography - e.g. reuse of legacy code
- use of masterkeys (key gives root permissions) only during development

e.g. in small websites: sqllite (flat-file database) - data is stored in one file on the server -> can be downloaded and queried without access control
# Impact
- depends on data exposed, might be fatal
# Defence
- classify all data stored and transferred
- only store sensitive data that is really necessary
- use encryption/secure protocols for transfer
- store data encrypted
- set access restrictions

