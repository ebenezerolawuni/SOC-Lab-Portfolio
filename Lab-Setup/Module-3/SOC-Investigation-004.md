# SOC Investigation 004 — Windows Firewall Registry Value Deleted

## Summary
Wazuh recorded a registry value deletion in the Windows Firewall Rules registry area on the SOC-WIN11 endpoint.

## Event Details
- **Date:** 14 October 2026
- **Time:** 13:12:30.754
- **Event:** Registry Value Entry Deleted
- **Registry Path:** `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\FirewallRules`
- **Deleted Value:** `{F6E3E0BA-019F-4B90-862A-041DE5769C4D}`

## Analysis
The event confirms that a registry value was deleted from the Windows Firewall Rules area. The available evidence does not identify the specific firewall rule or the process responsible for the deletion.

## Assessment
**Status:** Cause unconfirmed.

The event may relate to a legitimate configuration change, but unauthorised activity cannot be ruled out from this evidence alone.

## Recommended Follow-up
If further investigation is required, correlate the timestamp with nearby Windows Security and Sysmon events to identify the process or account associated with the change.

## Learning Outcome
Learned how to use Wazuh File Integrity Monitoring (FIM) alerts to identify and document registry value deletions.
