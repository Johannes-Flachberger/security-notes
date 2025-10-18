**Tags:** #type/tool #tactic/reconnaissance/passive  
**Link:** https://trufflesecurity.com/trufflehog
**Purpose:** search for sensitive information in git repos

---
# Info
Guide: https://trufflesecurity.com/blog/scanning-git-for-secrets-the-2024-comprehensive-guide

# Usage
scanning a git repo - all git platforms are supported
`trufflehog git <REPO_URL>`

scanning a github org
`trufflehog github --org=trufflesecurity --results=verified,unknown`

Scan all repos of a github user: https://github.com/SecDev0ps/mass_trufflehog/tree/main

