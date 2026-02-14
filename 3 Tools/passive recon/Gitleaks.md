---
tags:
  - "#type/tool" 
  - "#attack/reconnaissance/passive" 
Link: https://github.com/gitleaks/gitleaks
Purpose: Scan local git repos for credentials
---
# Info

Scan a local [[2 Tech-Specifics/Dev/git|git]] repo for credentials

Cannot scan remote repos - only local ones --> first clone then scan

Support for github actions

# Usage

in repo root directory run: `gitleaks detect`
