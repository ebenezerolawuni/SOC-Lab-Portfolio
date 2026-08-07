# Incident Report 001 - User Logoff Analysis

## Alert Information

- Platform: Wazuh SIEM
- Agent: Ebenezer (Windows 11)
- Rule ID: 67023
- Severity Level: 3
- Event Type: User Logoff

## Description

Wazuh detected that a non-service user account logged off from the Windows endpoint.

## Investigation

The event was reviewed in the Wazuh Threat Hunting dashboard.

The activity occurred after testing Windows authentication events on the endpoint.

## Analysis

The event appears to be normal user activity.

No indicators of compromise were identified.

## Classification

Benign Activity

## Recommendation

Continue monitoring endpoint activity. Escalate only if unusual patterns such as repeated unexpected logoffs or suspicious user behaviour are detected.

## Status

Closed ✅
