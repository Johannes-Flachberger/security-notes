---
tags:
  - "#type/method" 
  - "#attack/credential-access" 
---
# Fundamentals
Two types:
- **Bruteforce Attacks** are usually not based on a wordlist but rather tries all possible permutations of an allowed list of characters
- **Dictionary Attacks** use wordlists that are tried sequentially 

Both types of attacks can be carried out against
- a remote system using a specific protocol
- a local file, e.g. a password hash

**Note:** Attacks can also involve trying one password for multiple different usernames - this is also called _password spraying_.
## Wordlists
A wordlist required for dictionary attacks.
Use existing wordlists. See:
- [[3 Tools/bruteforce/seclists|seclists]]
- in kali, see `/usr/share/wordlists`
- popular in CTFs: `/usr/share/wordlists/rockyou.txt`
Generate a custom Wordlist. See:
- [[1 Methods/Security-Testing/2 Ressource Development/Overview - 2 Ressource Development#Wordlist generation|Generate Wordlists]]
# Pentesting

> [!HINT] Hint
> Some applications have default user names, which are rarely changed - even if the default password has been changed. This is often the case for web applications.
## Workflow
1. Prepare [[#Wordlists]]
2. Either perform a remote or local attack
## Remote Attacks
- [[3 Tools/bruteforce/Hydra|Hydra]]
- [[3 Tools/web/Burp Suite|Burp Suite]] Pro (for web applications)
## Local Attacks (Hash-cracking)
Tools for hash identification:
- LLMs
- [[3 Tools/crypto/hashID|hashID]]

Tools for hash cracking:
- [[3 Tools/crypto/Hashcat|Hashcat]]
- [[3 Tools/crypto/John the ripper|John the ripper]]