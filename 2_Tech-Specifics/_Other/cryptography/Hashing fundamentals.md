tags: #type/theory 

---
#todo add link to secure hashes/crypto eg https://www.keylength.com/
# Hashing
Hash structure:
`$format$rounds$salt$hash`
### Hash types
Windows: NTLM (look identical to md4 & md5), password hashes are stored in the SAM
Linux: shown in table, password hashes are stored in /etc/shadow file
`$1$`
md5crypt, used in Cisco stuff and older Linux/Unix systems
`$2$, $2a$, $2b$, $2x$, $2y$`
Bcrypt (Popular for web applications)
`$6$`
sha512crypt (Default for most Linux/Unix systems)

## resources:
Wordlists, Hashes,...
https://github.com/danielmiessler/SecLists/tree/master/Passwords

## salt and pepper
salt = random value attached to password vvefore hashing to prevent use of rainbow tables - salt is stored with the password hash
pepper = same as salt but stored externally