
# Phantom Installer CyberDefenders Blue Team Investigation

## Project Overview

This project documents a hands-on digital forensics and incident response investigation completed through the CyberDefenders platform.

The investigation focused on analyzing suspicious Windows executable files, examining forensic artifacts, reconstructing system activity, and identifying malicious behavior.

## Investigation Objectives

- Examine suspicious executable files and related artifacts.
- Analyze Windows file system and execution evidence.
- Investigate potential command-and-control activity.
- Identify indicators of compromise.
- Reconstruct relevant events using forensic tools.
- Document technical findings and security recommendations.

## Tools Used

- FTK Imager
- Event Viewer
- Detect It Easy
- dnSpy
- MFTECmd
- Timeline Explorer
- PECmd
- PowerShell and Command Prompt

## Investigation Status

**Status:** CyberDefenders lab completed.

Detailed methodology, findings, and supporting evidence will be added in the next documentation phase.


---

## Investigation Methodology

### 1. Forensic Evidence Examination

Used FTK Imager to examine Windows forensic artifacts and identify suspicious executable files associated with the investigation.

### 2. Suspicious File Analysis

Examined executable files associated with the suspicious installer, including:

- `update.exe`
- `ZoomSetupCode.payload.update.exe`
- `byebye.exe`
- `nftec.exe`

Used Detect It Easy and dnSpy during file analysis to examine executable characteristics and investigate potentially malicious functionality.

### 3. Windows Artifact Analysis

Investigated Windows execution and filesystem artifacts using:

- MFTECmd
- Timeline Explorer
- PECmd
- Windows Event Viewer

These tools supported examination of file metadata, execution evidence, and recorded system activity.

### 4. Timeline Reconstruction

Correlated available forensic timestamps and execution artifacts to investigate the sequence of suspicious activity.

The investigation focused on identifying the relationship between the suspicious installer, subsequent executable activity, and potential command-and-control or destructive behavior.

### 5. Findings and Reporting

Documented the investigation findings, relevant indicators, and security implications.

The investigation was performed as an authorized CyberDefenders Blue Team training exercise.

## Investigation Evidence

### Lab Completion

![CyberDefenders Phantom Installer Lab Completion](phantom-installer-lab-completion.png)

*Evidence of completed CyberDefenders Phantom Installer investigation.*

---

