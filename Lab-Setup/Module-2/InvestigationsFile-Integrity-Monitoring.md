# File Integrity Monitoring Investigation — Rule 553

## Overview

This investigation analysed a file deletion detected by Wazuh File Integrity Monitoring (FIM).

The objective was to determine what file was deleted, understand the significance of the event, and assess whether the activity represented malicious behaviour or controlled laboratory activity.

---

## Detection

**Rule ID:** 553

**Description:** File deleted

**Severity:** Level 7

**Timestamp:** August 11, 2026 — 15:45:15

---

## Evidence

```text
syscheck.path:
C:\soc-lab-test\soc-test.txt

syscheck.event:
deleted

syscheck.size_after:
16

syscheck.md5_after:
7c64334774047268751fb5c114e07772

syscheck.sha256_after:
9154384256ccaca64d412b23daa4ea90ec64140c3ccc74f5ebda5c80f82e581d

syscheck.uname_after:
eben
```

The monitored file was:

`C:\soc-lab-test\soc-test.txt`

The Wazuh FIM subsystem recorded the file deletion.

---

## Investigation

The first step was to identify the affected file and determine whether the deletion occurred within a monitored laboratory location.

The file was located under:

`C:\soc-lab-test\`

This directory was part of the controlled SOC laboratory environment.

The event was therefore considered in the context of the activity being performed in the lab rather than being treated automatically as a malicious deletion.

---

## Risk Assessment

A file deletion can be significant from a security perspective.

For example, an attacker could delete:

* Logs
* Evidence
* Security tools
* Configuration files
* Application data

However, the presence of a FIM deletion alert alone does not establish malicious intent.

The surrounding context must be investigated.

In this case, the deletion occurred within the controlled SOC testing environment and was associated with the laboratory exercise.

---

## Classification

**🟢 Benign / Controlled Lab Activity**

---

## Key SOC Lessons

1. FIM provides visibility into changes to monitored files.
2. A file deletion alert should be investigated rather than automatically classified as malicious.
3. File path and system context are important when assessing risk.
4. Controlled lab exercises can intentionally generate security alerts.
5. FIM can be useful for detecting attempts to remove or alter potentially important files.
6. The alert is the starting point; additional evidence is required to determine intent.

---

## Analyst Conclusion

Wazuh Rule 553 correctly detected the deletion of `C:\soc-lab-test\soc-test.txt`. The event was assessed as benign because the file was located within the controlled SOC laboratory environment and the deletion was part of the testing activity. The investigation demonstrated how FIM can provide visibility into file deletion events while requiring contextual analysis to determine their security significance.
