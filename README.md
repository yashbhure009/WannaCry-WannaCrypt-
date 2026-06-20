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

### Technical Findings
- **EternalBlue requires zero credentials** — just network access to port 445 is enough
  to gain full SYSTEM-level shell on an unpatched Windows 7 machine
- **SMBv1 is catastrophically dangerous** — a 2017 vulnerability still works perfectly
  on unpatched systems in 2026
- **WannaCry encrypts files in seconds** — by the time a human notices, the damage is done;
  automated detection is essential
- **SYSTEM-level access bypasses all user-level controls** — UAC, user permissions, and
  standard defenses are irrelevant once kernel exploitation succeeds

### Attacker Perspective
- The full attack chain (scan → exploit → shell → ransomware execution) took under 15 minutes
- Metasploit's EternalBlue module auto-detects architecture and OS — minimal attacker skill required
- A single open port (445) on an unpatched host was the only requirement for full compromise

### Defender Perspective
- **Patch Tuesday matters** — MS17-010 was patched in March 2017; unpatched systems 9 years
  later remain trivially exploitable
- Network segmentation would have contained the blast radius significantly
- Offline, tested backups are the only reliable recovery path from ransomware
- Disabling SMBv1 entirely (it has no legitimate modern use case) eliminates this attack surface

### Operational Mistakes Made During Lab
- Initially left `LHOST` as `127.0.0.1` (loopback) — reverse shell never connects back;
  always set LHOST to the actual attacker NIC IP
- Accidentally changed `RPORT` from 445 to 4444 — SMB always runs on 445
- These mistakes highlight the importance of verifying `show options` before running exploits

### Key Takeaway
> A single unpatched service exposed to the network is all it takes.
> Patch management, network segmentation, and offline backups are not optional —
> they are the minimum baseline for ransomware resilience.
