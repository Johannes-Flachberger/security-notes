---
tags:
  - "#type/tech-specific"
  - "#attack/initial-access/server-side"
  - "#attack/reconnaissance/active"
  - "#attack/exfiltration"
---
# Fundamentals

HTTP(S) - Hypertext Transfer Protocol (Secure)

**Default Ports:**

- tcp80 (HTTP)
- tcp443 (HTTPS)

## HTTP Authorization

### Basic authorization

Username & password are transmitted base64 encoded in a HTTP header in `<username>:<password>` format

# Pentesting

## Enumeration

See [[2 Tech-Specifics/Web/Enumeration - Web/Overview - Enumeration - Web|Overview - Enumeration - Web]]

## Execution

See [[2 Tech-Specifics/Web/Attacks - Web/Overview - Attacks - Web|Overview - Attacks - Web]]

## Exfiltration

E.g. using:

- [[3 Tools/file-transfer/updog|updog]]
- [[3 Tools/file-transfer/simple python webserver|simple python webserver]]
- [[3 Tools/file-transfer/raven|raven]]

# Hardening
