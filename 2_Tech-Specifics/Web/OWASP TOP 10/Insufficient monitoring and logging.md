**Type:** #type/theory
**Tags:** #goal/exploitation 

---

- important actions are not logged, e.g. successful logins, unsuccessful logins, database errors,...
- warning & errors are not logged with enough detail e.g. request is logged, but not the content which would show that somebody tried an Sql injection
- logged data is not scanned for suspicious activity
- penetration tests which cause a ot of noise do not cause an alarm

### Impact
- You dont even notice that you are attacked
- if you notice an attack ou can react - if an attacker notices this they will stop most probably
### Defense
- log all relevant events with ** all relevant information**
- store log messages in format which ccan be scanned automatically
- use automatic scanning for suspicous behavior