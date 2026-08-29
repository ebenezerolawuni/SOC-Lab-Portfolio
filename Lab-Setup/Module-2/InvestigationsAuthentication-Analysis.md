# Authentication Failure Investigation — Rule 60122

## Overview

This investigation analysed Windows authentication failure events detected by Wazuh.

The objective was to determine whether the failed authentication attempts represented normal lab activity, suspicious behaviour, or a potential brute-force attack.

---

## Detection

**Rule ID:** 60122

**Description:** Logon Failure — Unknown user or bad password

**Severity:** Level 5

---

## Events Investigated

### Event 1

**Timestamp:** August 7, 2026 — 13:04:50

```text
Target User: EBENEZER$
Domain: WORKGROUP
Source IP: 127.0.0.1
Logon Type: 2
Status: 0xc000006d
Sub-status: 0xc0000380
```

### Event 2

**Timestamp:** August 7, 2026 — 15:54:01

```text
Target User: EBENEZER$
Domain: WORKGROUP
Source IP: 127.0.0.1
Logon Type: 2
Status: 0xc000006d
Sub-status: 0xc0000380
```

### Event 3

**Timestamp:** August 20, 2026 — 18:45:20

```text
Target User: wronguser
Domain: ebenezer
Source IP: ::1
Logon Type: 2
Status: 0xc000006d
Sub-status: 0xc0000064
Workstation: EBENEZER
```

---

## Investigation

The events were compared based on:

* Target username
* Domain
* Source IP
* Logon type
* Authentication status
* Sub-status
* Frequency and timing
* Known laboratory activity

The first two events involved the account:

`EBENEZER$`

The third event involved:

`wronguser`

The target accounts were therefore different.

The source addresses were also technically different:

* `127.0.0.1` — IPv4 loopback
* `::1` — IPv6 loopback

Both addresses represent the local host rather than a remote external system.

The third event also contained sub-status `0xc0000064`, which is associated with an unknown/non-existent user account.

---

## Brute-Force Assessment

The events did not demonstrate the characteristics of a sustained brute-force attack.

There was:

* No large volume of repeated failures within a short period
* No evidence of a remote source
* No evidence of multiple password attempts against a valid account
* No indication of coordinated authentication activity

The `wronguser` event was also known to have been generated as part of controlled SOC laboratory testing.

---

## Classification

**🟢 Benign / Expected Activity**

The authentication failures were assessed as controlled laboratory activity rather than a brute-force attack.

---

## Key SOC Lessons

1. Failed authentication does not automatically indicate an attack.
2. Source IP addresses must be interpreted in context.
3. `127.0.0.1` and `::1` are loopback addresses representing the local system.
4. Different usernames can indicate different authentication contexts.
5. Authentication status and sub-status codes provide additional investigative evidence.
6. Frequency and timing are important when assessing potential brute-force activity.
7. Controlled security testing can intentionally generate authentication failures.

---

## Analyst Conclusion

The investigated Rule 60122 events were assessed as benign and consistent with controlled SOC lab activity. The events originated from the local Windows system and involved different authentication contexts rather than a sustained pattern of remote failed authentication attempts.
