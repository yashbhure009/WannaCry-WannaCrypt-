# WannaCry-WannaCrypt-
# WannaCry Ransomware Simulation

## Disclaimer
This project was conducted in an isolated lab environment for educational and defensive cybersecurity purposes only.

## Objective
Understand ransomware behavior, detection opportunities, and incident response procedures.

## Lab Environment
- Windows VM(s)
- Isolated virtual network
- Snapshot-enabled environment

## Overview
WannaCry is a ransomware family that spread rapidly in 2017 by abusing a Windows SMB vulnerability. This simulation reproduces key observable behaviors in a controlled environment.

## Observations
- File encryption activity
- SMB-related network traffic
- Process creation events
- Security log artifacts

## Detection Opportunities
- Unusual SMB activity
- Mass file modifications
- Suspicious process execution

## Mitigations
- Disable SMBv1
- Apply security updates
- Maintain offline backups
- Network segmentation

## Lessons Learned
