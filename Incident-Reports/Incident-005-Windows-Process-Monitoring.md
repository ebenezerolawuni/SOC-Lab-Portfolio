# Incident Report 005 - Windows Process Monitoring

## Alert Information

* Platform: Wazuh SIEM
* Agent: Ebenezer (Windows 11)
* Monitoring Technology: Sysmon
* Rule ID: 92000
* Description: Scripting interpreter spawned a new process
* Severity Level: 4
* Timestamp: 11 August 2026 @ 18:18:58.877

## Observed Activity

Wazuh detected a Windows command shell spawning the `tasklist.exe` process.

### Process Information

**Image:**

```text
C:\Windows\System32\tasklist.exe
```

**Command Line:**

```text
C:\Windows\system32\cmd.exe /d /s /c "tasklist /FI "IMAGENAME eq BlueStacks X.exe""
```

The command checks whether the `BlueStacks X.exe` process is running.

## Investigation

The activity was reviewed as part of a controlled SOC laboratory exercise.

The command uses the legitimate Windows `tasklist.exe` utility to query running processes. The executable is located in the standard Windows System32 directory.

The activity therefore does not provide sufficient evidence of malicious behaviour.

## Assessment

**Classification:** Benign / Legitimate Activity

**Risk:** Low

The Wazuh alert was triggered because a command shell spawned another process. This behaviour can occur during normal application or system activity and is not, by itself, evidence of compromise.

## SOC Analyst Response

No containment or remediation was required.

The alert was reviewed and classified as benign based on the available process and command-line information.

## Lessons Learned

* Sysmon Event ID 1 provides useful process-creation telemetry.
* Parent-child process relationships are important during SOC investigations.
* Wazuh rules identify potentially interesting behaviour but do not automatically mean an attack has occurred.
* Analysts should examine the executable path, command line, parent process and context before classifying an alert.

## Status

Closed
