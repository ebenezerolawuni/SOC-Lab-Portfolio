# Incident Report 006 - Windows Command Shell Activity

## Alert Information

* Platform: Wazuh SIEM
* Agent: Ebenezer
* Monitoring Technology: Sysmon
* Rule ID: 92052
* Description: Windows command prompt started by an abnormal process
* Severity Level: 4
* Timestamp: 11 August 2026 @ 20:05:54.681
* Sysmon Event ID: 1 - Process Create

## Observed Activity

Wazuh detected `cmd.exe` being launched by the BlueStacks Services application.

### Process Chain

```text
BlueStacksServices.exe
        ↓
     cmd.exe
        ↓
   tasklist.exe
```

### Process Information

**Image:**

```text
C:\Windows\System32\cmd.exe
```

**Parent Image:**

```text
C:\Users\ebene\AppData\Local\Programs\bluestacks-services\BlueStacksServices.exe
```

**Parent Command Line:**

```text
"C:\Users\ebene\AppData\Local\Programs\bluestacks-services\BlueStacksServices.exe" --hidden
```

**Command Line:**

```text
C:\Windows\system32\cmd.exe /d /s /c "tasklist /FI "IMAGENAME eq BlueStacks X.exe""
```

The command checks whether `BlueStacks X.exe` is currently running.

## Investigation

The alert was investigated using Sysmon process-creation information from Wazuh.

The parent process was identified as `BlueStacksServices.exe`, located within the user's BlueStacks installation directory. The child process was the legitimate Windows `cmd.exe`, which executed the standard `tasklist` utility to check for the BlueStacks X process.

No evidence of malicious payload execution, persistence, or suspicious command-line activity was identified from this event.

## Assessment

**Classification:** Likely Benign / Legitimate Application Activity

**Risk:** Low

The Wazuh rule generated an alert because a command shell was started by another process. Further investigation provided legitimate application context for the activity.

## SOC Analyst Response

No containment or remediation was required.

The alert was reviewed and classified as likely benign based on the available process relationship, executable paths and command line.

## Lessons Learned

* Sysmon Event ID 1 records process creation.
* Parent-child process relationships are important when investigating alerts.
* Command-line information provides useful context.
* A Wazuh alert does not automatically indicate malicious activity.
* Background applications can generate alerts that require investigation and classification.

## Status

Closed
