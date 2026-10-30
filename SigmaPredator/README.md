# SigmaPredator Windows Event Log Clearing Detection Engineering

## Project Overview

This project documents a hands-on detection engineering investigation completed through the CyberDefenders SigmaPredator lab.

The investigation focuses on identifying Windows Event Log Clearing techniques associated with attacker defense evasion and developing Sigma detection rules to identify suspicious activity.

## Scenario

As a Detection and Hunting Engineer at the fictional CyberPredator Enterprise, my objective is to research adversary techniques used to clear Windows event logs, identify relevant forensic artifacts, and develop detection rules to improve security monitoring.

## Project Objectives

- Investigate Windows Event Log Clearing techniques.
- Identify relevant Windows commands, PowerShell methods, and WMI activity.
- Analyze Windows process creation and security event logs.
- Develop Sigma detection rules.
- Validate detections using Chainsaw and historical EVTX logs.
- Document findings and recommend detection improvements.

## Tools and Technologies

- Sigma
- Chainsaw
- Visual Studio Code
- Windows Event Logs
- PowerShell
- MITRE ATT&CK

## Investigation Progress

### Phase 1: Technique Research

In progress.

### Phase 2: Sigma Rule Development and Validation

Not started.

## Evidence and Screenshots

Screenshots and detection results will be added throughout the investigation.

## Key Findings

To be completed after validating the detection rules.


## Lab Scenario

![SigmaPredator Lab Scenario](screenshots/01-lab-scenario.png)

## Technique Research

### Question 1 Process Creation Detection

The native Windows utility `wevtutil.exe` can be used to manage and clear event logs. Monitoring its execution helps identify suspicious log-clearing activity.

![Process Creation Detection](screenshots/02-wevtutil-process-creation.png)


### Question 2 WMI-Based Windows Event Log Clearing Detection

**Objective:** Identify the WMI component associated with clearing Windows event logs and understand how attackers can abuse it to remove security evidence.

**Technical Explanation:**

Windows Management Instrumentation (WMI) is a Microsoft technology that enables administrators to manage and monitor Windows operating systems.

Windows Management Instrumentation Command-line (WMIC) provides command-line access to WMI functionality.

The `nteventlog` WMIC alias maps to the `Win32_NTEventLogFile` WMI class, which provides functionality for managing Windows event logs.

**Example Command:**

```cmd
wmic nteventlog where "LogFileName='Security'" call ClearEventLog
```

This command demonstrates how the Windows Security event log can be cleared using WMI.

**Security Implications:**

Attackers may abuse legitimate Windows management tools to clear event logs, remove evidence of unauthorized activity, and complicate security investigations.

**Detection Engineering Approach:**

Security engineers can monitor Windows process creation events for suspicious commands containing:

- `wmic.exe`
- `nteventlog`
- `ClearEventLog`
- References to Security, System, or Application event logs

**Key Finding:**

WMI-based event log clearing represents an alternative method to using `wevtutil.exe`. Effective detection engineering requires monitoring multiple techniques attackers may use to remove evidence.

**MITRE ATT&CK:** T1070.001 Clear Windows Event Logs (lab classification).

### Screenshot Evidence Question 2

The following screenshot documents the WMI Process Creation Detection investigation conducted during the SigmaPredator lab.

![Question 2 - WMI Process Creation Detection](screenshots/03-wmi-process-creation.png)

*Figure 2: SigmaPredator Question 2 WMI Process Creation Detection.*


### Question 3 PowerShell Script Block Logging Detection

**Objective:** Identify the PowerShell logging mechanism and Windows Event ID used to monitor suspicious PowerShell execution associated with Windows event log clearing.

**Logging Feature:** PowerShell Script Block Logging

**Windows Event Channel:** `Microsoft-Windows-PowerShell/Operational`

**Event ID:** `4104`

#### Technical Explanation

PowerShell Script Block Logging is a Windows security logging feature that records the content of PowerShell scripts and commands during execution.

When Script Block Logging is enabled, Windows generates Event ID 4104 in the `Microsoft-Windows-PowerShell/Operational` event channel.

This provides security analysts with visibility into PowerShell activity and helps identify suspicious commands that attackers may execute to clear Windows event logs.

#### Example of Suspicious Activity

```powershell
Clear-EventLog -LogName Application
```

This command clears entries from the Windows Application event log.

Although this functionality can be used for legitimate administrative purposes, attackers may abuse it to remove evidence of malicious activity.

#### Detection Engineering Approach

Security engineers can develop Sigma rules to analyze PowerShell Script Block Logging events for suspicious commands associated with event log manipulation.

Relevant indicators include:

- `Clear-EventLog` Clears entries from specified Windows event logs.
- `Remove-EventLog` Deletes specified classic Windows event logs or unregisters event sources.
- `EventLogSession.ClearLog()` A .NET method that can clear Windows event logs.

Monitoring Event ID 4104 allows security teams to identify potentially suspicious PowerShell code and investigate whether the activity was authorized.

#### Security Implications

Attackers may attempt to clear Windows event logs to reduce forensic visibility and conceal unauthorized activities.

PowerShell Script Block Logging provides an additional detection opportunity beyond monitoring process creation events alone.

#### Key Findings

PowerShell Script Block Logging and Event ID 4104 provide important visibility into PowerShell-based event log manipulation.

Detection engineers should combine PowerShell telemetry with process creation events and Windows event log clearing indicators to improve detection coverage and reduce reliance on a single data source.

**MITRE ATT&CK:** T1070.001 Clear Windows Event Logs (classification used in the SigmaPredator lab).

#### Screenshot Evidence

The screenshot below documents Question 3 of the SigmaPredator Detection Engineering investigation.

![Question 3 - PowerShell Script Block Logging Detection](screenshots/04-powershell-script-block-logging.png)

*Figure 3: Investigation of PowerShell Script Block Logging and Windows Event ID 4104 during the SigmaPredator lab.*
