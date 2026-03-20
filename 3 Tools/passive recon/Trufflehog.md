---
tags:
  - "#type/tool" 
  - "#attack/reconnaissance/passive"  
Link: https://trufflesecurity.com/trufflehog
Purpose: search for sensitive information in git repos
---
# Info

Search for sensitive information in remote or local git repos. It can also verify discovered credentials by trying to use them (e.g. trying a found [[2 Tech-Specifics/Cloud/AWS/Fundamentals - AWS|AWS]] access key)

# Usage

**Guide:** [Trufflehog Blog](https://trufflesecurity.com/blog/scanning-git-for-secrets-the-2024-comprehensive-guide)

scan a remote git repo - all git platforms are supported:

`trufflehog git <REPO_URL>`

scan a local git repo:

`trufflehog git file://<repo_path>`

scan a github org:

`trufflehog github --org=trufflesecurity --results=verified,unknown`

Scan all repos of a github user: <https://github.com/SecDev0ps/mass_trufflehog/tree/main>
