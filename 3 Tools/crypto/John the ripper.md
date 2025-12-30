---
tags:
  - "#type/tool" 
  - "#attack/credential-access" 
Link: https://www.openwall.com/john/
Purpose: hashcracking
---
# Info

# Usage

## Workflow

1. Prepare the hash file
2. Run john with appropriate options
3. Show cracked passwords

## Command

`john [options] [hash file]`

| Option                | Purpose                                                          |
| --------------------- | ---------------------------------------------------------------- |
| `--wordlist=[path]`   | specify wordlist for dictionary attack                           |
| `--format=[format]`   | specify the hash format                                          |
| `--list=formats`      | list all supported hash formats                                  |
| `--show`              | display all cracked passwords                                    |
| `--single`            | use single crack mode for word mangling                          |
| `--rules=<rule name>` | use custom rules for word mangling - see [[#Rule-based attacks]] |
| `--test`              | run benchmark                                                    |

## Rule-based Attacks

rules are defined in `/etc/john/john.conf`

Use `[List.Rules:<ruleName>]` to mark the rule

**Note:** Rule are generally compatible with [[3 Tools/crypto/Hashcat|Hashcat]]

Reference: <https://www.openwall.com/john/doc/RULES.shtml>

## Conversion Tools

There are many conversion tools located at: `/usr/share/john/`

**zip files:** `zip2john [options] [zip file] > [output file]`
**rar archives:** `rar2john [rar file] > [output file]`
**ssh private key files:** `ssh2john [id_rsa private key file] > [output file]`
if command is not found look for ssh2john script in `/usr/share/john/ssh2john.py`
