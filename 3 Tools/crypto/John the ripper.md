**Tags:** #type/tool #tactic/credential-access 
**Link:** https://www.openwall.com/john/
**Purpose:** hashcracking

---
# Info

# Usage

**automatic cracking:**
`john --wordlist=[path to wordlist] [path to file]`
**format specific cracking**
`john --format=[format] --wordlist=[path to wordlist] [path to file]`
**list hash formats**
`john --list=formats` to list all formats `| grep -iF "keyword"` to filter output
**show all cracked passwords**
`john --show [password hash file]`

**word mangling**
use option `--single`
**custom rules**
custom rules, eg. for word mangling are defined in /etc/john/john.conf
https://www.openwall.com/john/doc/RULES.shtml
**cracking zip files**
`zip2john [options] [zip file] > [output file]`
**cracking rar archives**
`rar2john [rar file] > [output file]`
**cracking ssh private key files**
`ssh2john [id_rsa private key file] > [output file]`
if command is not found look for ssh2john script in `/usr/share/john/ssh2john.py`
there are loads of conversion tools for different purposes in the `/usr/share/john/` folder