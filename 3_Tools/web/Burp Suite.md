**Type:** #type/tool
**Tags:**  #goal/exploitation
**Link:** [https://portswigger.net/burp/communitydownload](https://portswigger.net/burp/communitydownload) 
**Purpose:** professional webhacking framework

---
# Info
very common webapp testing framework
Burp always works a proxy between your browser (or the built in browser) and the target --> you can perform manual requests and then edit, mutate, etc. them with Burps Modules

**Tipps:**
- has keyboard shortcuts - see global options
- has also a darkmode
- if the webpage hangs, while loading, "intercept" might be enabled in burpsuites proxy settings
- use default browser and foxy proxy for a user friendly setup
- 

# External Browser Setup
 If you want to use an external browser, e.g because you want to use other tools or browser extensions in parallel, you need to set burp as a proxy and install its CA certificate for TLS interception
 See https://portswigger.net/burp/documentation/desktop/external-browser-config
# Modules
## Proxy
- redirects web browser traffic thorugh burp suite
configured to “intercept” traffic: requests can be modified, dropped, repeated,…
- also respones can be intercepted (proxy options)
- use match and replace to automatically replace certain things in the requests
## Target
sitemap: gathers resources of the target
scope: specify the scope (target) of the tests
## Repeater
modify and repeat requests manually
## Intruder
carry out automated attacks (fuzzing), eg. bruteforcing sql injections
in positions tab, set the parts you want to fuzz
Payload: set wordlists, e.g. [[3_Tools/bruteforce/seclists|seclists]]
### attack modes
**Sniper**
tries every word of a word list --> good for single position attacks
with multiple positions: tries everything on 1st position, then on 2nd position,...
**Battering ram**
like sniper, bit with multiple positions puts the same parameter in each position
**Pitchfork**
takes multiple payload sets (1 for each position) and iterates through them all at once (1 request will use 1st item of all the lists, 2nd request 2nd item,...)
**Cluster bomb**
multiple positions, multiple payload sets - tries every possible combination
eg. Bruteforcing user & password combinations
### Result Analysis
distinguish successful results from unsuccessful ones by
a) response code
b) response length (most of the times: shorter request = successfull)
when bruteforcing using POST requests, there might be no difference in length or status code -> then you can search for keywords, e.g. welcome, or something you know is on the login success page
## Sequencer
analyze the randomness of unpredictable items, eg. session tokens
you can capture you tokens/cookies live by sending a request to sequencer or load them manually
## Decoder
encode and decode data in various formats
## Extender
load 3rd party or own modules
modules are invoked in descending order
eg. download requests from de BApp store - there are modules written in java and python (some steps are necesarry to acctivate python support - just google)

info for own modules:
https://portswigger.net/burp/extender/writing-your-first-burp-suite-extension