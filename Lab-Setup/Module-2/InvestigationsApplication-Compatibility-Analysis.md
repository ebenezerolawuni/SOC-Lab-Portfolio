# Application Compatibility Database Investigation — Rule 92058

## Overview

This investigation analysed a high-severity Wazuh alert involving the Windows Application Compatibility Database.

The objective was to determine why the event was detected, identify the process responsible, examine its parent process and service context, and determine whether the activity was malicious or legitimate Windows behaviour.

---

## Detection

**Rule ID:** 92058

**Description:** Application Compatibility Database launched

**Severity:** Level 12

**Timestamp:** August 25, 2026 — 15:45:42

---

## Evidence

### Process

```text
Image:
C:\Windows\System32\sdbinst.exe
```

### Command Line

```text
C:\Windows\System32\sdbinst.exe -m -bg
```

### Parent Process

```text
C:\Windows\System32\svchost.exe
```

### Parent Command Line

```text
C:\Windows\system32\svchost.exe
-k LocalSystemNetworkRestricted
-p
-s PcaSvc
```

### User

```text
NT AUTHORITY\SYSTEM
```

---

## Investigation

The first step was to identify the executable associated with the alert.

The process was:

`sdbinst.exe`

The executable was located in:

`C:\Windows\System32\`

The next step was to identify the parent process.

The parent was:

`svchost.exe`

The parent command line showed that the process was associated with the Windows service:

`PcaSvc`

This service is associated with the Windows Program Compatibility Assistant.

---

## Process Relationship

The process chain was:

```text
svchost.exe
      ↓
PcaSvc
      ↓
sdbinst.exe
```

The presence of a Windows system service as the parent process provided important context for the alert.

---

## Severity Assessment

The alert was assigned **Level 12**, which indicates that the detection logic considered the activity highly significant.

However, severity should not be treated as proof of malicious behaviour.

The investigation therefore focused on the actual evidence.

The process:

`sdbinst.exe`

was a legitimate Windows system executable located in:

`C:\Windows\System32\`

The parent process and service context were also consistent with normal Windows functionality.

---

## Classification

**🟢 Benign / Expected Windows Activity**

---

## Key SOC Lessons

1. A high-severity alert requires investigation but does not automatically mean an attack occurred.
2. The executable path should be checked when investigating process execution.
3. Parent processes provide important context.
4. Windows system services can legitimately launch processes that appear suspicious to detection rules.
5. Command-line arguments can help explain why a process was executed.
6. Rule severity should be considered alongside the underlying evidence.
7. A SOC analyst should avoid making a final classification based solely on the alert description.

---

## Analyst Conclusion

Wazuh Rule 92058 generated a Level 12 alert when `sdbinst.exe` was executed. Investigation of the executable path, command line, parent process and associated `PcaSvc` service provided evidence consistent with legitimate Windows Program Compatibility Assistant activity.

Although the alert was high severity, the available evidence did not indicate malicious behaviour.

The event was therefore classified as:

**Benign / Expected Activity**
