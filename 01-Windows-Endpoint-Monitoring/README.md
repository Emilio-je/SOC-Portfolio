# SOC Lab 01 --- Windows Endpoint Monitoring with Wazuh and Sysmon

## Overview

This project documents the construction of a defensive SOC home lab
focused on Windows endpoint monitoring, process telemetry, alert triage,
investigation, and MITRE ATT&CK mapping.

The lab uses a Windows 11 endpoint monitored by Sysmon and the Wazuh
Agent, with events centralized in a Wazuh Manager, Indexer, and
Dashboard.

## Objectives

-   Build an isolated Windows security monitoring environment.
-   Collect Windows endpoint telemetry with Sysmon.
-   Forward Sysmon events through the Wazuh Agent.
-   Centralize and visualize events in Wazuh.
-   Investigate Process Creation events.
-   Perform basic SOC alert triage.
-   Map detections to MITRE ATT&CK.
-   Document findings as an analyst would in an operational SOC.

## Architecture

``` text
Windows 11 Endpoint
SOC-WIN11-01
192.168.56.102
       |
       | Sysmon Event Channel
       v
Wazuh Agent
       |
       | TCP 1514
       v
SOC-WAZUH-01
192.168.56.104
       |
       +--> Wazuh Manager
       +--> Wazuh Indexer
       +--> Wazuh Dashboard
```

Network: `192.168.56.0/24` Host-Only network.

## Technologies

-   VirtualBox
-   Windows 11
-   Ubuntu Server
-   Wazuh 4.14.x
-   Wazuh Agent
-   Microsoft Sysmon
-   PowerShell
-   MITRE ATT&CK

## Lab Status

-   [x] Wazuh server deployed
-   [x] Windows endpoint deployed
-   [x] Wazuh Agent installed
-   [x] Sysmon installed
-   [x] Sysmon event collection configured
-   [x] Agent connected to Wazuh Manager
-   [x] Sysmon Event ID 1 visible in Wazuh
-   [x] Controlled PowerShell activity generated
-   [x] Alert triaged
-   [x] MITRE ATT&CK mapping identified
-   [ ] Detection engineering
-   [ ] Threat hunting
-   [ ] Incident response exercise

## First Investigation

A controlled PowerShell process was generated:

``` powershell
powershell.exe -Command "Write-Host 'SOC LAB TEST'"
```

Sysmon generated Event ID 1 (Process Create), which was collected by the
Wazuh Agent and displayed in the Wazuh Dashboard.

Wazuh triggered rule `92027`:

> Powershell process spawned powershell instance

The event was mapped to:

-   Tactic: Execution
-   Technique: T1059.001 --- PowerShell

### Triage conclusion

The alert was classified as **Benign / Lab Test** because the activity
was intentionally generated during the investigation and the executable
was the expected Windows PowerShell binary.

## Evidence

Screenshots and exported evidence should be stored in:

`Evidence/`

Do not store passwords, API keys, tokens, private keys, or other secrets
in this repository.

## Analyst Workflow

``` text
Detect
  ↓
Triage
  ↓
Investigate
  ↓
Correlate
  ↓
Map to MITRE ATT&CK
  ↓
Determine
  ↓
Document
```

## Future Improvements

-   Add a curated Sysmon configuration.
-   Create custom Wazuh detection rules.
-   Investigate suspicious PowerShell behavior.
-   Add network telemetry.
-   Perform threat hunting.
-   Create incident response playbooks.
-   Add IOC extraction and enrichment.
-   Document additional MITRE ATT&CK techniques.
