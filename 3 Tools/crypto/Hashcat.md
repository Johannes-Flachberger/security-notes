---
tags:
  - "#type/tool" 
  - "#attack/credential-access"
Link: https://hashcat.net/hashcat/
Purpose: hashcracking
---
# Info
> [!warning] Since hashcat is GPU based, it may not work properly in VMs.
# Usage
find hash mode numbers on: [https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)
## Workflow
1. put hashes to be cracked in file
2. run hashcat
3. cracked hashes are in the potfile or in output file if specified

`./hashcat.exe -m [hash mode number] -a [attack mode] [hash file] [wordlist file]`

| Option             | Purpose                                                                                                                                                                                                                                         |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-b`               | benchmark the present hardware & compare the hash rate with no. of possible combinations - see [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks#Time Estimation\|Bruteforce and Dictionary Attacks]] |
| `-o [output file]` | specify output file                                                                                                                                                                                                                             |
| `-O`               | use optimized kernel code - limits password length to 27 chars                                                                                                                                                                                  |
| `-r <path>`        | path to rule file, for based attacks                                                                                                                                                                                                            |
| `--stdout`         | print attempted passwords - used for debugging of rulesets                                                                                                                                                                                      |
## Rule-based attacks
Create, or mutate the wordlist based on specified criteria.

E.g: `hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt -r append.rule`

Rules are provided using a file. Each line contains a set of rules which are applied to each password in the list.
**Hint:** A lot of functions are compatible with the rule-engines other tools, such as [[3 Tools/crypto/John the ripper|John the ripper]] 

Reference: https://hashcat.net/wiki/doku.php?id=rule_based_attack
Useful rules are located in: `/usr/share/hashcat/rules`

**Example:**
```
$1 c $!
$2 c $!
$1 $2 $3 c $!
```