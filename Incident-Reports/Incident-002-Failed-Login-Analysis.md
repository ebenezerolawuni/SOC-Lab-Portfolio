# Incident Report 002 - Failed Login Analysis

## Alert Information

- Platform: Wazuh SIEM
- Agent: Ebenezer (Windows 11)
- Windows Event ID: 4625
- Event Type: Failed Login Attempt

## Description

Wazuh detected failed Windows authentication attempts caused by an unknown username or incorrect password.

## Investigation

The event was identified using Windows Security Event ID 4625 in the Wazuh Threat Hunting dashboard.

The activity was generated intentionally to test endpoint monitoring and alert detection.

## Analysis

The failed login attempts were confirmed as part of a controlled SOC lab exercise.

No evidence of malicious activity was identified.

## Classification

Benign Testing Activity

## Recommendation

Continue monitoring authentication events.

Investigate further if multiple failed login attempts occur from unknown users, unusual locations, or are followed by successful access.

## Status

Closed ✅
