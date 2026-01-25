---
tags:
  - "#type/tech-specific" 
---

#todo add link to secure hashes/crypto eg <https://www.keylength.com/>

# Hashing

Hash structure:

`$format$rounds$salt$hash`

### Hash Types

- **Windows:** NT hashes (also called NTLM hashes) - look identical and are similar to md4 & md5 - NT hashes are **not salted** --> weak!
- **Linux:** password hashes are stored in /etc/shadow file
- `$1$`: md5crypt, used in Cisco stuff and older Linux/Unix systems
- `$2$, $2a$, $2b$, $2x$, $2y$`: Bcrypt (Popular for web applications)
- `$6$`: sha512crypt (Default for most Linux/Unix systems)

## Salt and Pepper

**salt** = random value attached to password before hashing to prevent use of rainbow tables - salt is stored with the password hash

**pepper** = same as salt but stored externally
