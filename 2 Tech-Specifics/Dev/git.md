---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

Very popular version control system.

## Git CLI Usage

| Purpose                        | Command                    |
| ------------------------------ | -------------------------- |
| show history graph             | `git log --graph`          |
| show commit details inkl. diff | `git show <commit_id>`     |
| checkout commit                | `git checkout <commit_id>` |

## CI/CD Pipelines

Usually CI/CD Pipeline definitions are included in a git repo, if any exist. Their format depends on the automation server used. For example:

- [[2 Tech-Specifics/Dev/Jenkins|Jenkins]]
- Github Actions
- etc.
If you can modify a pipeline definition, you can try to poison it to e.g. exfiltrate credentials or gain a reverse shell on the runner the pipeline is executed by.

# Pentesting

## Credential Access

 Sometimes credentials get pushed to git repos by accident. --> When obtaining access to a git repo, scan its whole history for sensitive data.

**Tools:**
- [[3 Tools/passive recon/Trufflehog|Trufflehog]]: scan **local** and **remote** repos & verify the discovered credentials
- [[3 Tools/passive recon/Gitleaks|Gitleaks]]: scan **local** repos

# Hardening
