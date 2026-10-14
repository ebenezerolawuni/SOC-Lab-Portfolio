# Module 3 — SOC Investigation 001

## Successful Windows Service Logon

**Host:** SOC-WIN11  
**Wazuh Rule ID:** 60106  
**Windows Event ID:** 4624  
**Account:** SYSTEM  
**Logon Type:** 5 — Service logon

### Investigation
Wazuh recorded a successful Windows logon under the built-in SYSTEM account. Logon Type 5 indicates a service logon, which is consistent with normal Windows service activity.

### Assessment
No clear evidence of malicious activity was identified in the fields reviewed. The event appears consistent with routine Windows service activity.

### Disposition
No further action required based on this event alone.

**Status:** Investigated and documented.
