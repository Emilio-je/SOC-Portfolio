# Investigation --- Case 001

## Alert

**Rule:** 92027\
**Description:** Powershell process spawned powershell instance\
**Severity:** 4\
**Event ID:** Sysmon 1 --- Process Create

## Endpoint

-   Agent: `SOC-WIN11-01`
-   IP: `192.168.56.102`

## Observed Process

``` text
Image:
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

Command line:

``` text
powershell.exe -Command "Write-Host 'SOC LAB TEST'"
```

Parent process:

``` text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

## User Context

The event was executed under the Windows lab account recorded by Sysmon.

## Hash

The event contained a SHA256 hash for the PowerShell executable. Hash
values should be treated as evidence and should not be considered
malicious by themselves.

## Triage

### Initial concern

PowerShell is a legitimate Windows administration tool but is also
commonly monitored in SOC environments because attackers can abuse it
for execution and post-exploitation.

### Findings

-   The executable path was the expected Windows PowerShell location.
-   The publisher/company information identified Microsoft.
-   The command line matched the controlled test performed by the
    analyst.
-   The parent-child relationship was PowerShell → PowerShell.
-   No malicious behavior was introduced during this test.

## Verdict

**Benign --- Controlled SOC Lab Test**

## Analyst Lesson

The presence of PowerShell alone is not enough to classify an event as
malicious. Analysts should examine command line, parent process, user,
executable path, hashes, network activity, and surrounding events.
