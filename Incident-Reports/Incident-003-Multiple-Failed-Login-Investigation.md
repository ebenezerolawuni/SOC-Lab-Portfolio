# Incident Report 003 - Multiple Failed Login Investigation

## Alert Information

- Platform: Wazuh SIEM
- Agent: Ebenezer (Windows 11)
- Rule ID: 60122
- Severity Level: 5
- Event Type: Multiple Failed Login Attempts

## Description

Wazuh detected multiple failed Windows authentication attempts within a short period.

## Investigation

A total of 7 failed login attempts were observed.

The events were generated intentionally during a SOC lab exercise to validate Wazuh's authentication monitoring capabilities.

## Analysis

The repeated failed logins matched the expected behaviour of the test scenario.

No indicators of compromise or unauthorized access were identified.

## Classification

Benign Lab Activity

## Recommendation

Monitor for repeated failed logins in production environments.

Escalate if the attempts originate from unknown sources, target privileged accounts, or are followed by a successful login.

## Status

Closed ✅
