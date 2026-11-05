# File Integrity Monitoring: File Hash and Change Detection

## Overview

For this exercise, I used the Wazuh dashboard to review File Integrity Monitoring (FIM) activity from my Windows 10 Pro endpoint. The aim was to understand how Wazuh records changes to monitored files and how file hashes help an analyst investigate those changes.

FIM is useful because a file can be edited, created, or deleted without the change being obvious during normal use. Wazuh keeps information about monitored files and compares later observations with the recorded baseline. When it detects a relevant difference, it can generate an alert.

## Lab setup

- **SIEM:** Wazuh
- **Endpoint:** Windows 10 Pro
- **Endpoint agent:** Wazuh agent
- **Feature reviewed:** File Integrity Monitoring (Syscheck)

## What I observed

### 1. FIM events in the Wazuh dashboard

![Wazuh FIM events](../Screenshot%202026-11-05%20054005.png)

The events view shows activity reported by the Windows endpoint, including a file event described as **“Integrity checksum changed”** and several Windows Registry events, including deleted registry keys or values.

The checksum-change event is important because it indicates that the monitored file's recorded integrity information no longer matches its previous baseline. The dashboard also displays the event time, endpoint name, file or registry path, rule description, rule level, and rule ID.

These events are evidence of detected changes. They do not, by themselves, prove that an attacker made the changes. In a real investigation, I would check whether the activity was expected, identify the user or process involved where that information is available, and compare it with approved system or software changes.

### 2. File inventory and hash information

![Wazuh monitored file details](../Screenshot%202026-11-05%20054022.png)

The file details view shows metadata collected for a monitored text file. The information includes:

- File size
- Last analysis and last modified timestamps
- User associated with the file
- MD5, SHA-1, and SHA-256 hash values
- File permissions

A cryptographic hash acts like a digital fingerprint of the file's contents. If the contents change, the hash will normally change as well. SHA-256 is the hash value I would give the most attention to when documenting file integrity.

The screenshot shows the hash values recorded for the file at the time of the inventory view. The events screenshot separately shows a checksum-change alert. These two views together demonstrate how I can review a FIM finding and inspect the file metadata associated with it. They are not a before-and-after pair of hash values, so I am not presenting them as proof of the exact old and new hash.

## What I learned

- Wazuh FIM can report changes to monitored files and Windows Registry entries.
- A checksum-change alert is a useful starting point for investigating whether a file's contents have changed.
- The file inventory provides useful context, including timestamps, size, permissions, and cryptographic hashes.
- Registry changes can be legitimate, so alerts need to be reviewed in context rather than treated as automatic proof of compromise.
- Monitoring only applies to the files, directories, and registry locations included in the agent's FIM configuration.

## How I would investigate an unexpected change

1. Confirm the affected endpoint and the exact file or registry location.
2. Review the event timestamp and compare it with the user's activity or approved maintenance window.
3. Check available user and process information to understand what made the change.
4. Compare the current file hash with a trusted baseline or known-good copy.
5. Record the finding and escalate or investigate further if the change is not authorized.

## Outcome

This exercise gave me practical experience reviewing FIM events in Wazuh and inspecting file integrity metadata on a Windows endpoint. It helped me connect the idea of a file checksum with the alerts a SOC analyst may need to investigate.

*This was a hands-on exercise in my home lab. The screenshots show the events and file details available in my environment at the time of testing.*
