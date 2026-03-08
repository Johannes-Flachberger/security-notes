---
tags:
  - "#type/tool"
  - "#attack/reconnaissance/active"
Link: https://www.zaproxy.org/
Purpose: web application vulnerability scanner
---
# Info

- if a webapp is really vulnerable, OWASP ZAP might corrupt it
- it can give some overview about the vulnerabilites, but always misses some stuff
- proxy listener on 127.0.0.1 port 8080 - so it can conflict with [[3 Tools/web/Burp Suite|Burp Suite]]

# Usage

1. open zap and enter the URL, then click start
2. spidering results are under the "Spider" tab
3. vulnerabilities found are under the "Alerts" tab
