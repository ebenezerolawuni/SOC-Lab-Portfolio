# SOC Investigation 005 — Failed Windows Logon

## Summary
Wazuh recorded one failed Windows logon event on the SOC-WIN11 endpoint.

## Event Details
- **Date:** 14 October 2026
- **Time:** 19:45:01.198
- **Windows Event ID:** 4625
- **Subject Username:** `ebene`
- **Status:** `0xc000006d` — Logon failure
- **Substatus:** `0xc000006a` — Incorrect password
- **Logon Type:** 2 — Interactive logon

## Analysis
The event indicates that an interactive logon attempt failed due to incorrect authentication information. The substatus identifies an incorrect password as the reported reason. The subject username is `ebene`, but the failed target account was not identified in the available fields.

## Assessment
**Status:** Inconclusive — further context required.

A single failed logon may result from a typing error or another authentication issue. There is insufficient evidence to classify this event as malicious.

## Recommended Follow-up
If necessary, review nearby Windows Security events for repeated failures or a subsequent successful logon, and identify the target account.

## Learning Outcome
Learned how to interpret Windows Event ID 4625, status codes, substatus codes, and logon types in Wazuh.

