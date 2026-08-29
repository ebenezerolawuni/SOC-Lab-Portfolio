# 🛡️ SOC Lab Portfolio

## About Me

Hi, I'm Ebenezer.

I'm building a hands-on Security Operations Center (SOC) lab to develop practical cybersecurity skills and prepare for a SOC Analyst role.

This portfolio documents my practical learning journey, including SOC lab deployment, SIEM monitoring, Windows endpoint investigation, security alert analysis, and incident investigation.

---

## Lab Environment

| Component        | Technology             |
| ---------------- | ---------------------- |
| Operating System | Windows 11             |
| SIEM             | Wazuh                  |
| Linux Server     | Ubuntu Server          |
| Virtualisation   | VMware Workstation Pro |

---

## Lab Architecture

```text
Windows 11 Endpoint
        │
        │ Wazuh Agent
        ▼
Ubuntu Server
        │
        ▼
Wazuh Manager
        │
        ▼
Wazuh Dashboard
```

---

# 📚 Training Progress

## Module 1 — SOC Lab Foundations

**Status: ✅ COMPLETE**

Completed practical work including:

* SOC lab setup
* Ubuntu Server deployment
* Server preparation
* Wazuh SIEM installation
* Windows endpoint integration
* Wazuh Agent configuration
* Initial security monitoring

---

## Module 2 — SOC Alert Investigation & Incident Analysis

**Status: ✅ COMPLETE**

Module 2 focused on analysing real endpoint telemetry and developing an evidence-based SOC investigation methodology.

### Key Areas Investigated

* Wazuh security alerts
* Windows authentication failures
* File Integrity Monitoring (FIM)
* Registry integrity monitoring
* Windows process execution
* CMD execution
* PowerShell-related telemetry
* Parent-child process relationships
* Command-line analysis
* Event correlation
* Detection versus evidence
* Benign activity and false-positive assessment
* Windows system activity

### Key Wazuh Rules Investigated

| Rule ID | Detection                                             | Assessment                 |
| ------- | ----------------------------------------------------- | -------------------------- |
| 553     | File deleted                                          | 🟢 Controlled lab activity |
| 60122   | Logon Failure                                         | 🟢 Benign / controlled     |
| 750     | Registry Value Integrity Checksum Changed             | 🟢 Benign / expected       |
| 92032   | Suspicious Windows cmd shell execution                | 🟢 Benign / expected       |
| 92052   | Windows command prompt started by an abnormal process | 🟢 Benign / expected       |
| 92058   | Application Compatibility Database launched           | 🟢 Benign / expected       |

### Investigation Methodology

The investigations followed an evidence-based workflow:

```text
Security Alert
      ↓
Review Alert Details
      ↓
Identify Supporting Evidence
      ↓
Analyse Process / Event Context
      ↓
Examine Parent-Child Relationships
      ↓
Review Command Line
      ↓
Correlate Related Events
      ↓
Assess User & System Context
      ↓
Determine Risk
      ↓
Final Classification
```

### Key Lesson

A security alert is a **starting point for investigation**, not automatically proof of malicious activity.

During Module 2, alerts were assessed using supporting evidence such as process relationships, command lines, usernames, timestamps, file paths, registry paths and system context.

---

## 📋 Incident Reports

### Completed

* ✅ Incident 001 — User Logoff Analysis
* ✅ Incident 002 — Failed Login Investigation
* ✅ Incident 003 — Multiple Failed Login Investigation

### Module 2 Investigation Reports

* ✅ Authentication Failure Investigation
* ✅ File Integrity Monitoring Investigation
* ✅ Registry Integrity Investigation
* ✅ Windows Process Execution Investigation
* ✅ Application Compatibility Investigation
* ✅ Module 2 Final Assessment

See the **Module-2** folder for the detailed investigation reports.

---

# 🧠 Skills Demonstrated

### SOC & SIEM

* SIEM monitoring
* Wazuh administration
* Alert investigation
* Security event analysis
* Event correlation
* Incident assessment

### Windows Security

* Windows Event Logs
* Sysmon telemetry
* Authentication analysis
* Process execution analysis
* Parent-child process analysis
* Command-line investigation
* Registry monitoring
* File Integrity Monitoring

### Investigation

* Evidence-based analysis
* Detection versus evidence
* False-positive identification
* Benign activity classification
* Timeline analysis
* Process-tree analysis
* Risk assessment

### Technical

* Ubuntu Server administration
* VMware Workstation Pro
* Windows endpoint configuration
* Wazuh Agent configuration
* Troubleshooting
* Technical documentation

---

# 🔬 Current Progress

### ✅ Module 1 — SOC Lab Foundations

Completed.

### ✅ Module 2 — SOC Alert Investigation & Incident Analysis

Completed.

### 🔜 Module 3 — Advanced Endpoint Monitoring & Threat Hunting

Next.

Planned areas include:

* Dedicated Windows security VM
* Sysmon configuration
* Advanced Windows telemetry
* PowerShell monitoring
* Process investigation
* Threat hunting
* Controlled security testing
* Malware-analysis fundamentals
* Email-analysis exercises
* Detection engineering
* Practical TryHackMe exercises

---

## 📸 Screenshots

See the **Screenshots** folder for evidence of the SOC lab environment, Wazuh dashboard, endpoint configuration and security investigations.

---

# 🎯 Career Goal

My goal is to develop practical, evidence-based SOC Analyst skills through hands-on laboratory exercises, security investigations and continuous documentation.

This portfolio represents my progression from building a SOC environment to investigating endpoint security events and developing practical incident-response and threat-hunting skills.
