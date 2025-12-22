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
A wordlist is required for dictionary attacks. There are 2 Options:
1. Use existing wordlists - see:
	- [[3 Tools/bruteforce/seclists|seclists]]
	- in kali, see `/usr/share/wordlists`
	- popular in CTFs: `/usr/share/wordlists/rockyou.txt`
2. Generate a custom wordlist - see:
	- [[1 Methods/Security-Testing/2 Ressource Development/Overview - 2 Ressource Development#Wordlist generation|Generate Wordlists]]
# Pentesting

> [!HINT] Hint
> Some applications have default user names, which are rarely changed - even if the default password has been changed. This is often the case for web applications.
## Remote Attacks
> [!Warning] 
> Dictionary & Bruteforce Attacks generate a lot of noise - they are easily detected, and often blocked by modern applications
### Workflow
1. Prepare [[#Wordlists]]
2. Either perform a remote or local attack
### Tools:
- [[3 Tools/bruteforce/Hydra|Hydra]]
- [[3 Tools/web/Burp Suite|Burp Suite]] Pro (for web applications)
## Local Attacks (Hash-cracking)
### Workflow
1. Extract hashes
2. Format hashes
3. [[#Time Estimation|Estimate the cracking time]]
4. Prepare [[#Wordlists]]
	- in most cases it is advised to apply rule-based mutations to wordlists 
5. Get cracking
### Tools
**Hash identification**
- LLMs
- [[3 Tools/crypto/hashID|hashID]]
- [hash-identifier](https://www.kali.org/tools/hash-identifier/)

 **Hash cracking**
- [[3 Tools/crypto/Hashcat|Hashcat]]: faster, but more complex
	- Primarily GPU-based, also supports CPU
	- requires GPU drivers
- [[3 Tools/crypto/John the ripper|John the ripper]]: slower, but simpler
	- Primarily CPU-based, also supports GPU
### Time Estimation
Parameters:
- k: size of the keyspace, i.e. all possible characters within the password
- l: password length

Possible combinations = k^l 
--> compare the number of combinations e.g. with the hash rate of [[3 Tools/crypto/Hashcat|Hashcats]] benchmark.