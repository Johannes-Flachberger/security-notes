**Tags:** #type/method #tactic/initial-access/client-side 

---
# Introduction
Two types:
- Spear-Phishing: targets one specific person
- Broad-Phishing: targets lots of different people
Depending of the medium used, people use various terms:
- vishing: voice phishing
- smishing: sms phishing
Phishing can have **various objectives**:
- stealing credentials
- running malicious code

> [!HINT] **LLMs are strong at phishing**
> They can:
> - Automate search for information and possible targets
> - Automate the creation of mails, messages,...
> - Translate
> - Create fake voices and deepfakes

# Pentesting

> [!WARNING] At each step, keep the [[2 Tech-Specifics/People/Social Engineering#Psychological Principles|Psychological Principles]] behind social engineering in mind.

## Overview
The basis of the phishing campaign is a good pretext.
The pretext shall:
- align with the targets expectations
- fit into the targets context

The **basic components** of a phishing campaign are:
- a medium: e.g. email, sms, chat-apps, social media, voice, video
- a source: e.g. the source email address, phone number, account
- content: tells the target what to do 
- payload: documents, forged webpages, executables,...

All of the components can be optimised using fundamental [[2 Tech-Specifics/People/Social Engineering#Psychological Principles|Psychological Principles]] of social engineering.
## Workflow
### 1. Create a good Pretext
Perform in-depth [[1 Methods/Security-Testing/1 Reconnaissance/Overview - 1 Reconnaissance|Reconnaissance]] on the target. Here, LLMs and especially [RAG](https://cloud.google.com/use-cases/retrieval-augmented-generation) can be very helpful.

**Some classic pretexts:**
- CEO gift card
- CEO fraud - financial
- company tech auction - be fast!
### 2. Prepare the components
#### Medium
Use a familiar and legitimate communication channel.
Consider usage of multiple communication channels.

When using [[2 Tech-Specifics/_Other/Email|Email]], consider common email filtering techniques:
- sender domain reputation
- attachments (file extensions, contents,...)

For **voice interaction**, consider AI voice cloning
- e.g. https://elevenlabs.io/voice-cloning
#### Source
Make the source appear as credible as possible.
- e.g. use a legitimate mail address whose credentials were stolen or leaked
- for vishing, consider caller ID spoofing
#### Payload
Consider the following aspects:
- design (familiarity, legitimacy)
- language (familiarity)
##### Forged Webpages
**optimize the design:**
- see [[2 Tech-Specifics/Web/Webpage Cloning|Webpage Cloning]]
**optimize the URL**
- use [[2 Tech-Specifics/People/typo squatting|typo squatting]] to resemble a legitimate mail address, e.g. of a company or big providers such as google, microsoft,... 
	- Password Manager extensions can detect typosquatting
	- use an URL shortener to obfuscate the link
	- use [homograph URLs](https://en.wikipedia.org/wiki/IDN_homograph_attack)

To enhance credibility, use HTTPs - if possible with a valid certificate

a forged webpage can be used to exploit vulnerabilities in adjecient systems:
- perform [[2 Tech-Specifics/Web/WebApp Attacks/Cross Site Request Forgery (CSRF)|Cross Site Request Forgery (CSRF)]]
- orce NTLM authentication to steal the password hash
- link to an SMB server to steal the NTLM password hash
Also see [[2 Tech-Specifics/People/MFA bypass|MFA bypass]]

##### Malicious Files 
**Hints**
- phishy file types are often filtered on corporate mail servers
- also look out for file parsing vulnerabilities within [[2 Tech-Specifics/Client-Side Applications/Overview - Client-Side Applications|Client-Side Applications]], e.g. in popular pdf readers that could be exploited
- [[2 Tech-Specifics/OS/Windows/library-ms Files|library-ms Files]] are often not filtered, an less well-known and can be used as a 1st stage payload, to deliver further client side execution payload

Lots of different file types can be used to achieve client-side code execution:
```query
tag:#tactic/execution/client-side
```
Further:
- exe - often filtered, and quite obvious
- Jscript