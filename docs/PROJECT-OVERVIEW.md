# Project Overview
## SOC Home Lab — Scope, Goals, and Status

## 1. Introduction

This project builds a small virtual environment for learning the practical work of a Security Operations Centre (SOC). It focuses on the foundations: virtual machines, Linux administration, Windows endpoints, remote access, and preparing a SIEM workflow.

The lab is intentionally incremental. A component is treated as operational only after a meaningful verification step has been recorded.

## 2. Learning Goals

- Install and administer Ubuntu Server.
- Understand user accounts and SSH authentication.
- Create a Windows endpoint VM and practise remote administration.
- Learn the role of Wazuh in collecting, correlating, and presenting security telemetry.
- Build a repeatable process for verifying data collection and investigating security events.
- Maintain clear technical documentation suitable for future troubleshooting and portfolio review.

## 3. Environment

| Item | Recorded configuration |
|---|---|
| Host platform | Windows computer |
| Hypervisor | VMware Workstation Pro 17 |
| Linux VM | Ubuntu Server 24.04.1 LTS |
| Linux remote access | OpenSSH Server; Windows PowerShell as client |
| Windows VM | Windows 10 |
| Windows remote access | Remote Desktop Connection |
| SIEM interface | Wazuh dashboard |
| Network | VMware virtual networking; exact mode and topology should be documented during verification |

Specific local IP addresses are intentionally represented as placeholders in public documentation.

## 4. Work Completed

### Ubuntu Server
Ubuntu Server 24.04.1 LTS was installed in VMware Workstation. A hostname and local account were configured during installation. OpenSSH Server was enabled to support remote administration.

### SSH access
The Ubuntu guest's address was identified with `ip -br addr`. A connection was initiated from Windows PowerShell, the server host fingerprint was checked at the first connection prompt, and the Ubuntu account was used to authenticate. A welcome message and shell prompt confirmed the remote session.

### Windows endpoint
A Windows 10 VM was created and its desktop startup was checked. The VM is intended to provide endpoint activity for later monitoring exercises.

### RDP
The Windows network configuration was checked with `ipconfig`, and Remote Desktop Connection was opened with the target address. The workflow reached the Windows Security credential prompt. A successful interactive desktop session has not yet been confirmed in the recorded notes.

### Wazuh
The official Wazuh site and installation documentation were reviewed, and the Wazuh dashboard was accessed. The current notes do not yet prove that the Windows endpoint is enrolled, that events are arriving, or that detections have been validated.

## 5. Out of Scope for the Current Verified State

The following are goals, not claims of completion:

- Production deployment or enterprise scale.
- Confirmed Windows or Linux agent enrollment.
- Verified end-to-end event ingestion.
- Tested custom detection rules or alert delivery.
- Automated response or SOAR workflows.
- Compliance certification or production hardening.

## 6. Success Criteria

The next stage will be considered verified when:
1. RDP access is tested and the result is recorded.
2. The Wazuh component topology and service health are documented.
3. The Windows endpoint is visible as active in Wazuh.
4. A controlled test event appears in the expected search view.
5. At least one detection is validated with its evidence and limitations documented.

## 7. Project Method

Use a verify-as-you-go process: make one change, test it, capture the result, then proceed. This keeps network, authentication, endpoint, and SIEM problems distinguishable rather than debugging multiple layers at once.
