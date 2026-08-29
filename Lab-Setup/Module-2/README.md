# Module 2 — SOC Alert Investigation & Incident Analysis

## Overview

Module 2 focused on developing practical Security Operations Centre (SOC) investigation skills using **Wazuh**, Windows Event Logs, Sysmon data, and File Integrity Monitoring (FIM).

The objective was to move beyond simply reading security alerts and learn how to investigate the underlying evidence, correlate events, identify process relationships, and determine whether activity was benign, suspicious, or potentially malicious.

---

## Learning Objectives

By the end of Module 2, I developed practical experience in:

* Investigating Wazuh security alerts
* Understanding Wazuh rule IDs and severity levels
* Analysing Windows authentication failures
* Investigating File Integrity Monitoring (FIM) events
* Analysing registry modifications
* Understanding parent-child process relationships
* Investigating Windows CMD and PowerShell activity
* Correlating multiple security events
* Distinguishing security detections from supporting evidence
* Identifying potential false positives and benign activity
* Producing reasoned SOC analyst assessments

---

## Tools & Technologies

* **Wazuh**
* **Wazuh FIM / Syscheck**
* **Windows 11**
* **Windows Event Logs**
* **Sysmon**
* **PowerShell**
* **Windows Command Prompt**
* **MITRE ATT&CK concepts**

---

## Key Investigations

### 1. Authentication Failure Investigation — Rule 60122

**Detection:** Logon Failure — Unknown user or bad password

The investigation examined failed authentication events involving:

* `wronguser`
* `EBENEZER$`
* Local loopback addresses `127.0.0.1` and `::1`
* Logon Type 2
* Windows authentication status and sub-status codes

The events were assessed in context rather than being automatically classified as brute-force activity.

**Assessment:** Benign / controlled lab activity.

**Key lesson:** A failed authentication event is an indicator requiring investigation, not automatic proof of malicious activity.

---

### 2. File Deletion Investigation — Rule 553

**Detection:** File deleted

A controlled file deletion was investigated using Wazuh FIM.

Example monitored file:

`C:\soc-lab-test\soc-test.txt`

The investigation examined the file path, event type, and available integrity information.

**Assessment:** Controlled lab activity.

**Key lesson:** FIM provides visibility into changes to monitored files and can provide valuable evidence during incident investigations.

---

### 3. Registry Integrity Investigation — Rule 750

**Detection:** Registry Value Integrity Checksum Changed

An Active Setup registry value was identified:

`HKLM\Software\Microsoft\Active Setup\Installed Components\{9459C573-B17A-45AE-9F64-1857B5D58CEE}`

The affected value was:

`StubPath`

Further investigation revealed that the value pointed to:

`C:\Program Files (x86)\Microsoft\Edge\Application\...\Installer\setup.exe`

The executable and installation path were consistent with Microsoft Edge configuration activity.

**Assessment:** Benign / expected activity.

**Key lesson:** A registry modification can appear suspicious at first but may be legitimate software installation or configuration activity. The actual registry value must be investigated before making a final assessment.

---

### 4. Suspicious CMD Execution — Rule 92032

**Detection:** Suspicious Windows cmd shell execution

Several Rule 92032 alerts were investigated.

One recurring process chain was:

`chrome.exe → cmd.exe → WCChromeNativeMessagingHost.exe`

The command line referenced Adobe Acrobat's Chrome native messaging component.

The activity was correlated with the parent process, command line, user account, and previous observations.

**Assessment:** Benign / expected application activity.

**Key lesson:** The word **"Suspicious"** in a detection rule does not mean the activity is malicious. Process relationships and command-line evidence provide important context.

---

### 5. Abnormal CMD Execution — Rule 92052

**Detection:** Windows command prompt started by an abnormal process

The investigation examined the process responsible for launching `cmd.exe` and correlated the event with related Rule 92032 alerts.

The process context was consistent with the previously investigated Chrome/Adobe native messaging activity.

**Assessment:** Benign based on the available evidence.

**Key lesson:** Rule severity and rule descriptions should not be treated as final verdicts.

---

### 6. Application Compatibility Database — Rule 92058

**Detection:** Application Compatibility Database launched

Evidence included:

* `sdbinst.exe`
* Windows System32 directory
* Parent process: `svchost.exe`
* Service: `PcaSvc`
* User: `NT AUTHORITY\SYSTEM`

The process relationship was consistent with Windows Program Compatibility Assistant activity.

**Assessment:** Benign / expected Windows activity.

**Key lesson:** Legitimate Windows system processes can trigger high-severity detections depending on the detection logic. Process context is essential.

---

## Detection vs Evidence

One of the most important concepts learned during Module 2 was the difference between a **detection** and **evidence**.

### Detection

A detection is an automated alert generated when system activity matches a rule, signature, or behavioural condition.

### Evidence

Evidence consists of the underlying system artefacts used to determine what actually happened.

Examples include:

* Process image
* Parent process
* Parent command line
* Command line arguments
* Username
* IP address
* File path
* Registry path
* File hashes
* Timestamps
* Event IDs

A detection therefore acts as a **starting point for investigation**, rather than automatically proving malicious activity.

---

## Investigation Methodology

The investigation workflow developed during Module 2 was:

```text
Security Alert
      ↓
Examine Alert Details
      ↓
Identify Relevant Evidence
      ↓
Analyse Process / Event Context
      ↓
Check Parent-Child Relationships
      ↓
Review Command Line
      ↓
Correlate Related Events
      ↓
Consider User and System Context
      ↓
Determine Risk
      ↓
Benign / Suspicious / Potentially Malicious
```

---

## Module 2 Final Assessment

The final assessment involved analysing multiple Wazuh alerts occurring around the same time.

The investigation demonstrated the ability to:

* Compare alert severity with actual evidence
* Build a process execution chain
* Correlate multiple alerts
* Identify legitimate Windows activity
* Distinguish separate process chains
* Avoid classifying activity as malicious based solely on a rule description

### Final Assessment

**Result: PASS**

The incident scenario was assessed as:

**Benign / Expected Activity**

The conclusion was based on the available process relationships, command-line evidence, application context, and previously observed legitimate behaviour.

---

## Key Lessons Learned

1. **A high-severity alert does not automatically mean an attack occurred.**
2. **Detection rules are indicators, not final verdicts.**
3. **Parent-child process relationships are valuable investigative evidence.**
4. **Command-line analysis can reveal what a process was actually doing.**
5. **Registry modifications require contextual investigation.**
6. **FIM alerts show that something changed, but further investigation is required to determine whether the change was malicious.**
7. **Authentication failures should be assessed using frequency, account, source, logon type, and context.**
8. **Multiple alerts occurring at the same time should be correlated carefully rather than automatically treated as one incident.**
9. **Legitimate applications can trigger security detections.**
10. **A SOC analyst should base the final assessment on evidence rather than the alert description alone.**

---

## Next Phase

After completing Module 2, the next phase of the SOC lab will introduce a dedicated Windows virtual machine for controlled security testing.

Planned technologies and activities include:

* Windows VM
* Sysmon
* Wazuh Agent
* Process monitoring
* PowerShell monitoring
* Controlled security events
* Malware-analysis fundamentals
* Email-analysis exercises
* Threat hunting
* TryHackMe practical exercises

The goal is to progress from analysing pre-existing endpoint events to **generating and investigating controlled security events in a dedicated lab environment**.

---

**Module 2 Status: COMPLETE**
