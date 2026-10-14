# Module 3 — SOC Investigation 002

## Windows Firewall Registry Value Deleted

**Host:** SOC-WIN11  
**Date:** 14 October 2026  
**Timestamp:** 13:12:30.754  
**Event Description:** Registry Value Entry Deleted  
**Registry Change:** Deleted

### Registry Path
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\FirewallRules`

### Deleted Value
`{F6E3E0BA-019F-4B90-862A-041DE5769C4D}`

### Investigation
Wazuh File Integrity Monitoring detected the deletion of a registry value in the Windows Firewall rules registry location.

### Assessment
The change may relate to a firewall rule being removed or application configuration being updated. However, the reason for the deletion and its impact on firewall protection have not been confirmed.

### Disposition
**Status:** Investigated; cause unconfirmed. No conclusion of malicious activity can be made from the available evidence alone.

### Learning Point
Registry changes affecting Windows Firewall settings should be reviewed in context before being classified as benign or malicious.
