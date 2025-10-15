**Type:** #type/tool
**Tags:**  #tactic/reconnaissance/active  #tactic/reconnaissance/passive 
**Link:** https://github.com/OJ/gobuster
**Purpose:** enumaration of varios things - subdomains, directories, s3 buckets, etc

---
# Info
enumerate website directories, subdomains, etc
brute force, makes use of wordlist, in kali some are located in /usr/share/wordlists/dirbuster
# Usage
## directory enum
`gobuster dir -u http://<IP>:[port] -w <wordlist>`
eg: `gobuster dir -u http://<IP>:[port] -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

> [!NOTE]
> if a server return redirect code when a page is not found, you need to
> - add the HTTP status code to the "negative" codes in gobuster: `-b, --status-codes-blacklist` e.g. `-b 301`
> - or match the response lenght: `--exclude-length 0`
> 
## subdomain enum
`gobuster dns -d example.com -w wordlist.txt -t 10`
## patterns
^eab456
gobuster can mutate each entry in a wordlist with one or more patterns
1. create a pattern file - e.g:
```
{GOBUSTER}/v1
{GOBUSTER}/v2
```
{gobuster} matches each entry in the wordfile
2. use the pattern file using the `-p <pattern-file>` option. 
## options:
`-u`: target url
`-e`: print full urls in console
`-w`: path to wordlist
`-U` and `-P`: username and password for basic authentications
`-p <file>`: pattern file to use
`-c <cookies>`: specify cookie 
`-t`: number of threads

**alternatives**
- ffuf
- dirb
- dirbuster
