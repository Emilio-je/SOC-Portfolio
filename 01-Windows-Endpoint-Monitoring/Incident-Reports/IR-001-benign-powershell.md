# Incident Report --- IR-001

## Summary

A Sysmon Process Creation event generated a Wazuh alert after a
controlled PowerShell command was executed on the Windows 11 lab
endpoint.

## Classification

**Benign / Authorized Lab Activity**

## Timeline

1.  Analyst generated a controlled PowerShell command.
2.  Sysmon recorded Event ID 1.
3.  Wazuh Agent collected the Sysmon event.
4.  Wazuh Manager processed the event.
5.  Wazuh rule 92027 generated an alert.
6.  Analyst reviewed process, command line, parent process, user,
    executable path, and MITRE mapping.
7.  Alert was classified as benign.

## Detection

-   Sysmon Event ID: `1`
-   Wazuh Rule: `92027`
-   MITRE ATT&CK: `T1059.001`
-   Tactic: `Execution`

## Impact

No impact. The activity was intentionally generated for training.

## Response

No containment or remediation was required.

## Lessons Learned

This exercise demonstrated the complete workflow from endpoint telemetry
to SIEM alerting and analyst triage.

The key lesson is that a detection is an investigation starting point,
not proof of compromise.
