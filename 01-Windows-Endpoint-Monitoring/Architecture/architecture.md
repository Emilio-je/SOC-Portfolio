# Architecture

## Network

Host-Only network:

-   Network: `192.168.56.0/24`
-   Wazuh server: `192.168.56.104`
-   Windows endpoint: `192.168.56.102`

## Components

### SOC-WAZUH-01

Ubuntu Server running:

-   Wazuh Manager
-   Wazuh Indexer
-   Wazuh Dashboard

### SOC-WIN11-01

Windows 11 endpoint running:

-   Wazuh Agent
-   Microsoft Sysmon

## Data Flow

``` text
Windows Process
      ↓
Sysmon
      ↓
Windows Event Channel
      ↓
Wazuh Agent
      ↓ TCP 1514
Wazuh Manager
      ↓
Wazuh Indexer
      ↓
Wazuh Dashboard
```
