---
tags:
  - type/tool
Link: 
Purpose: popular editor with rich extension ecosystem
---
# Info
code-oss is the open source version - it has the core features but lacks some microsoft proprietory features like devcontainers

# Usage

# Snippets
In kali create the following launcher file at `~/.local/share/applications/code-oss-dev.desktop` to create an application launcher with the vscode icon:

```INI
[Desktop Entry]
Version=1.0
Type=Application
Name=code-oss
Comment=Start code-oss-dev
Exec=/usr/bin/code-oss
Icon=visual-studio-code
StartupWMClass=code-oss-dev
Path=~
Terminal=false
StartupNotify=false
```

