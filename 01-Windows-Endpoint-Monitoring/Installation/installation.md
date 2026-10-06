# Installation Notes

## Wazuh

Wazuh was deployed as an all-in-one installation on Ubuntu Server.

The server was configured with a Host-Only interface at:

`192.168.56.104`

## Wazuh Agent

The Windows endpoint was registered as:

`SOC-WIN11-01`

The Agent connects to the Wazuh Manager at:

`192.168.56.104`

The agent log confirmed:

``` text
Connected to the server ([192.168.56.104]:1514/tcp)
```

## Sysmon

Sysmon was installed on the Windows endpoint and verified with:

``` powershell
Get-Service Sysmon64
```

The service status was `Running`.

Sysmon telemetry was verified with:

``` powershell
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -MaxEvents 5
```

## Wazuh Sysmon Collection

The Wazuh Agent configuration was updated to collect:

``` xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

The agent log confirmed:

``` text
Analyzing event log: 'Microsoft-Windows-Sysmon/Operational'
```
