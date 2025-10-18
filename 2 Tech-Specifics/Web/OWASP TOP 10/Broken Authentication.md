**Tags:** #type/tech-specific

---

authentication methods are not secure.
Examples:
- weak passwords - use password validator, those are availably as simple libraries today
- no 2 step auth
- re-registration of users
- steal or guess session cookie - always invalidate session ids after logout
- no brute force protection - pause after x failed login attempts
- weak "reset password" process
- passwords stored as weak [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|hashes]]
- session ID is shown in URL
- default credentials are not deactivated

### Impact:
- attacker can login as regular user/admin
### Defence:
-  use brute force protection
-  enable 2 factor authentification
-  setup & **enforce** password policy
- generate session ids on server - everything that happens on the client can be reverse engineered