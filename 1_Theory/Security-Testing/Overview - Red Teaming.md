# Red Teaming vs Pentesting
Pentesting can be considered a subform of redteaming, however there are real differences: 

| **Aspect**       | **Red Teaming**                                                                                     | **Pentesting**                                                                  |
| ---------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Scope**        | Wide - tests a whole organisation including its processes, and ability to detect and react attacks. | Narrow - typically focused on a technical system, a range of IPs, etc.          |
| **Stealthyness** | Required                                                                                            | Not always required, sometimes just the defensive security measures are tested. |

There are a lot of pentesting processes out there, including very detailed models.
I decided to use [MITRE Att@ck](https://attack.mitre.org/ ) as a general framework for pentesting notes. Specificall, the tactics of MITRE Att@ck Enterprise Matrix are used as primary categorization. Inspired by the unified killchain, the tactics are grouped into three overall phases "In", "Through", and "Out". However, since MITRE Att@ck considers real-world cyber attacks, preparation and reporting phases need to be added to the structure.

This leads to the following structure:
- **Prep**
- **In**
	- 1 Reconnaissance
	- 2 Ressource Development
	- 3 Initial Access
	- 4 Execution
- **Through**
	- 5 Persistence
	- 6 Privilege escalation
	- 7 Defense evasion
	- 8 Credential-access
	- 9 Discovery
	- 10 Lateral Movement
- **Out**
	- 11 Collection
	- 12 Command and control
	- 13 Exfiltration
	- 14 Impact
- **Reporting**


