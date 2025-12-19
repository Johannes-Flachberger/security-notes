---
tags:
  - type/tech-specific 
  - attack/execution/client-side 
---
# Fundamentals

# Pentesting
## VBA Macros
### Challenges when using VBA macros
Often used in the past, but microsoft introduced various mitigations, making them less relevant today:
- Macros must be enabled manually when opening document
- If the [MoTW](https://en.wikipedia.org/wiki/Mark_of_the_Web) attribute is set, documents are opened in protected view by default - if a macro is included, a "security risk" banner is shown
	- Also see [MOTW Bypassing](https://attack.mitre.org/techniques/T1553/005/)
- many organizations might still use macros, but are well aware of their risk and strive to take countermeasures.
**Note:** These mitigations can be enforced using Active Directory Group Policies.
### Workflow
- E.g. create a word document and save the document as `.doc` to embed a macro within the file (`.docx` does not embed macros in the file)
- Create macro, choose the document as storage location.
- See [[2 Tech-Specifics/Client-Side Applications/VBA|VBA]] for details about visual basic scripting
# Hardening
