---
tags:
  - "#type/tool" 
  - "#attack/credential-access"
Link: https://hashcat.net/hashcat/
Purpose: hashcracking
---
# Info

# Usage

## Workflow

1. put hashes to be cracked in file
2. run hashcat
3. show results using `hashcat -m <mode> <hashfile>`

## Command

`hashcat -m [hash mode number] [hash file] [wordlist file]`

| Option             | Purpose                                                                                                                                                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-b`               | benchmark the present hardware & compare the hash rate with no. of possible combinations - see [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks#Time Estimation\|Bruteforce and Dictionary Attacks]] |
| `-o [output file]` | specify output file                                                                                                                                                                                                                    |
| `-O`               | use optimized kernel code - limits password length to 27 chars                                                                                                                                                                         |
| `-r <path>`        | path to rule file, for [[#Rule-based attacks]]                                                                                                                                                                                         |
| `--stdout`         | print attempted passwords - used for debugging of rulesets                                                                                                                                                                             |
| `--show`           | show cracked hash - also hashfile and mode are required<br>alternatively: show the whole potfile - default location on kali: `/root/.hashcat/hashcat.potfile`                                                                          |
| `-hh`              | print all hash mode numbers - can be searched - e.g. using [[3 Tools/utilities/grep\|grep]]                                                                                                                                            |
| `--identify`       | try to identify the right mode for a given hash                                                                                                                                                                                        |
| `-a`               | attack mode                                                                                                                                                                                                                            |
| `--username`       | tell hashcat that usernames are included in hash file in format `<username>:<hash>`                                                                                                                                                    |

find hash mode numbers on: [https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)

## Rule-based Attacks

Create, or mutate the wordlist based on specified criteria.

Reference: <https://hashcat.net/wiki/doku.php?id=rule_based_attack>

Rules are provided using a file. Each line contains a set of rules which are applied to each password in the list. Useful rules are located in `/usr/share/hashcat/rules` e.g.:

- `/usr/share/hashcat/rules/best66.rule`

E.g: `hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt -r append.rule`

**Hint:** A lot of functions are compatible with the rule-engines other tools, such as [[3 Tools/crypto/John the ripper|John the ripper]]

**Example:**

```
$1 c $!
$2 c $!
$1 $2 $3 c $!
```
