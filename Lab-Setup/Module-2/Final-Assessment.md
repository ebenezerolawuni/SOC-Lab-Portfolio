# Module 2 — Final SOC Assessment

## Assessment Overview

This assessment tested my ability to investigate multiple Windows security alerts using Wazuh and determine whether the observed activity represented malicious behaviour or legitimate system activity.

The assessment focused on:

* Alert severity
* Process relationships
* Command-line analysis
* Event correlation
* User context
* Distinguishing detections from evidence
* Final risk assessment

---

## Incident Timeline

### Alert 1 — Application Compatibility Database

**Timestamp:** August 25, 2026 — 15:45:42

**Rule ID:** 92058

**Severity:** Level 12

**Description:** Application Compatibility Database launched

**Image:**

`C:\Windows\System32\sdbinst.exe`

**Command Line:**

`sdbinst.exe -m -bg`

**Parent Process:**

`C:\Windows\System32\svchost.exe`

**Parent Command Line:**

`svchost.exe -k LocalSystemNetworkRestricted -p -s PcaSvc`

**User:**

`NT AUTHORITY\SYSTEM`

### Analysis

Although the alert had a high severity level, the severity alone did not establish malicious activity.

The process relationship and service context were consistent with Windows Program Compatibility Assistant activity.

---

## Alert 2 — Suspicious CMD Execution

**Timestamp:** August 25, 2026 — 15:46:03

**Rule ID:** 92032

**Severity:** Level 3

**Description:** Suspicious Windows cmd shell execution

**Image:**

`C:\Windows\System32\cmd.exe`

**User:**

`ebenezer\ebene`

### Analysis

The detection indicated that CMD execution matched the conditions of the Wazuh rule. However, additional evidence was required before determining whether the execution was malicious.

---

## Alert 3 — Chrome Launching CMD

**Timestamp:** August 25, 2026 — 15:46:03

**Rule ID:** 92032

**Severity:** Level 3

**Image:**

`C:\Windows\System32\cmd.exe`

**Parent Image:**

`C:\Program Files\Google\Chrome\Application\chrome.exe`

**Parent Command Line:**

`"C:\Program Files\Google\Chrome\Application\chrome.exe" --no-startup-window /prefetch:5`

**User:**

`ebenezer\ebene`

### Analysis

The parent-child relationship showed:

```text
chrome.exe
    ↓
cmd.exe
```

This was important evidence because it identified the application responsible for launching CMD.

---

## Alert 4 — Adobe Native Messaging Host

**Timestamp:** August 25, 2026 — 15:46:03

**Rule ID:** 92032

**Severity:** Level 3

**Image:**

`C:\Program Files\Adobe\Acrobat DC\Acrobat\Browser\WCChromeExtn\WCChromeNativeMessagingHost.exe`

**Parent Image:**

`C:\Windows\System32\cmd.exe`

**User:**

`ebenezer\ebene`

### Analysis

The process chain became:

```text
Chrome
   ↓
CMD
   ↓
Adobe Acrobat Native Messaging Host
```

This behaviour had previously been investigated in the SOC lab and was consistent with legitimate Chrome/Adobe integration.

---

## Detection vs Evidence

A key principle demonstrated during this assessment was the difference between a **security detection** and the **evidence used to assess the detection**.

A Wazuh rule indicates that activity matched a detection condition.

It does not automatically prove that malware or an attack occurred.

The investigation therefore considered:

* Process image
* Parent process
* Parent command line
* User account
* Command line
* Application context
* Timing
* Previously observed behaviour

---

## Correlation

Alerts 2, 3 and 4 occurred at essentially the same time and were linked through the process hierarchy.

The resulting process chain was:

```text
chrome.exe
    ↓
cmd.exe
    ↓
WCChromeNativeMessagingHost.exe
```

This correlation provided significantly more context than analysing Rule 92032 in isolation.

Alert 1 was investigated separately because its process chain involved:

```text
svchost.exe
    ↓
sdbinst.exe
```

and was associated with the Windows Program Compatibility Assistant.

---

## Final Assessment

### Classification

**🟢 Benign / Expected Activity**

### Reasoning

Although one alert generated a high Level 12 severity and other events were labelled "Suspicious," the underlying evidence did not demonstrate malicious activity.

The Application Compatibility Database event was consistent with Windows Program Compatibility Assistant activity.

The CMD alerts were associated with a Chrome → CMD → Adobe Acrobat native-messaging process chain that had previously been identified as legitimate application behaviour.

The final assessment was therefore based on the **available evidence and context rather than alert severity or rule descriptions alone**.

---

## Key SOC Lessons

* High severity does not automatically mean malicious activity.
* A detection should be treated as the beginning of an investigation.
* Parent-child process relationships provide valuable context.
* Command-line arguments can help identify the purpose of process execution.
* Related events should be correlated into a timeline or process chain.
* Separate process chains should not automatically be combined into one incident.
* Legitimate applications can trigger security detections.
* Final classifications should be evidence-based.

---

## Assessment Result

**PASS**

**Module 2 — SOC Alert Investigation & Incident Analysis**

The assessment demonstrated practical ability to investigate Windows security alerts, correlate endpoint evidence, analyse process relationships, and distinguish benign activity from potentially malicious behaviour.
