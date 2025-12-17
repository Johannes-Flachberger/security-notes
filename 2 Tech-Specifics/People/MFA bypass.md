---
tags:
  - type/tech-specific
---
# Fundamentals
Different types of multifactor authentication are used:
- push-based: the user just needs to "hit confirm" on the request
- code-based: the user needs to type in some code

# Pentesting
## Push-based
If push-based MFA is used, you can use "prompt bombing": Send authentication requests, until the target just accepts one to make it stop.
- see https://duo.com/blog/mfa-fatigue-what-is-it-how-to-respond
## Code-based
> [!HINT] Here, timing is critical, as authentication codes have a very short validity.

If the code needs to be typed in the webpage, fake the original user input field.
If the code needs to be typed in an authenticator app, you need to relay an legitimate authentication code from the original service.

Alternatively, use the browser-the-middle technique:
- requires a public IP address
- Tool: https://github.com/fkasler/cuddlephish
# Hardening
