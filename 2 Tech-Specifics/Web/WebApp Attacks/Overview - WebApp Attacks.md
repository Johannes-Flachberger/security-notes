---
tags:
  - "#type/tech-specific"
  - "#attack/exfiltration"
  - "#attack/execution/client-side"
  - "#attack/execution/server-side"
  - "#attack/initial-access/server-side"
---
# Overview

[[2 Tech-Specifics/Web/WebApp Attacks/OWASP TOP 10/Overview - OWASP TOP 10|Overview - OWASP TOP 10]] gives an overview of the most common webapp attack vectors. Altough frameworks use different technologies, they often apply the same principles - that leads to similar attack vectors across frameworks.

> [!NOTE]
> Browsers often optimize transfers, etc. for better UX -> this can get in the way when working with specifically crafted payloads. Better use [[3 Tools/web/cURL|cURL]] or [[3 Tools/web/Burp Suite|Burp Suite]]

# Techniques

```base
views:
  - type: table
    name: Table
    filters:
      and:
        - file.tags.contains("#type/tech-specific")
        - file.folder.startsWith(this.file.folder.toString()) && file.fullname != this.file.fullname

```

## Further Ideas:

[#todo](#todo)

Server Side request forgery by manipulating /etc/hosts or /etc/resolv.conf

# Payloads

**See:**

- <https://github.com/payloadbox>
- https://pentestmonkey.net/tools/web-shells/php-reverse-shell
