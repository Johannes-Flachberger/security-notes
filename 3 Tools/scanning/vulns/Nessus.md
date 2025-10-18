**Tags:** #type/tool #tactic/reconnaissance/active #tactic/discovery
**Link:** https://www.tenable.com/downloads/nessus
**Purpose:** commercial vulnerability scanner

---
# Info

UDP port scanning is disabled by default.

## Plugins
Plugins extend the default scan capabilities. Each individual vulnerability test is a plugin - like NVTs in OpenVAS. Plugin are grouped in families. See https://www.tenable.com/plugins/families/about.
## Templates
Docs: https://docs.tenable.com/nessus/Content/ScanAndPolicyTemplates.htm
A variety of predefined scan templates are available in Nessus. You can extend those using **Policies**.

**Template Categories**:
- Discovery
- Vulnerabilities
- Compliance (only available with paid license)

## Authenticated scanning
Lots of different protocols & authentication options are available
https://docs.tenable.com/nessus/Content/Credentials.htm
On windows, usually SMB or WMI is used.

Make sure that firewalls & antivirus software do not block the authenticated scan.
On windows, also UAC can influence the scan - see https://docs.tenable.com/nessus/Content/CredentialedChecksOnWindows.htm

### Useful templates
 - Basic Network Scan: good starting point, most settings are predefined
- Advanced Dynamic Scan: Selects plugins to be used automatically using a plugin filter.
- Credentialed Patch Audit: authenticated scan, only performs local checks, but no external scan
# Usage
## Setup
Download debian pacage from https://www.tenable.com/downloads/nessus
after installation start the service: `sudo systemctl start nessusd.service`
User interface available at: `https://127.0.0.1:8834`
## Workflow
1. Choose scan template
2. adjust configuration - e.g. targets, port list, scan options, credentials, schedule...
3. start scan
## Useful Scan Configurations
Docs: https://docs.tenable.com/nessus/Content/TemplateSettings.htm
Build a sitemap of a webapp: `Assessment > Web Applications > Scan Web Applications`