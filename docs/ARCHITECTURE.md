# SOC Home Lab Architecture

This page explains how the parts of my lab fit together and which connections I've tested so far.

## Basic setup

    Windows host
        |
    VMware Workstation
        |------------------|
    Ubuntu Server      Windows 10 VM
        |                  |
    SSH from PowerShell   Sysmon and Wazuh agent
                              |
                        Wazuh manager
                              |
                        Wazuh indexer
                              |
                        Wazuh dashboard

The Windows host runs the virtual machines. I have tested SSH access from PowerShell to Ubuntu and have seen the Windows Wazuh agent listed as Active in the dashboard. I still need to capture a specific Sysmon event in Wazuh to verify the complete event path.

## What each part does

| Component | Role in my lab | Current status |
|---|---|---|
| Windows host | Runs VMware and provides administration tools | In use |
| VMware Workstation Pro 17 | Runs the guest operating systems | Ubuntu and Windows VMs created |
| Ubuntu Server | Linux practice and Wazuh environment | Installed; SSH tested |
| PowerShell and SSH | Remote shell access to Ubuntu | Connection tested successfully |
| Windows 10 VM | Endpoint for Windows telemetry | Desktop started |
| Sysmon | Records selected Windows activity | Events visible locally in Event Viewer |
| Wazuh agent | Collects configured endpoint data | Windows agent shown as Active |
| Wazuh dashboard | Interface for searching and reviewing data | Accessible; specific event ingestion still needs testing |

## SSH and remote administration

For SSH, I check the current Ubuntu address and connect from PowerShell:

    ssh <ubuntu-username>@<ubuntu-lab-ip>

SSH provides an encrypted remote shell after the connection and authentication steps succeed. I treat SSH and RDP as administration tools; a working remote session doesn't prove that the SIEM is collecting events.

## How I expect the event path to work

1. Sysmon records selected Windows activity in the Sysmon Operational event channel.
2. The Wazuh agent must be configured to collect that channel.
3. The agent sends the collected data to the Wazuh manager.
4. Wazuh processes the incoming events and applies relevant rules.
5. The events and any resulting alerts can then be searched in the dashboard.

I have seen Sysmon events locally and have seen the Windows agent marked Active. I still need to locate a particular event in Wazuh before I can say that the full path has been verified.

## Keeping the lab safe

- Keep the virtual machines on the intended lab network.
- Verify an SSH host fingerprint when connecting to a machine for the first time.
- Restrict RDP and other management services to authorised lab systems.
- Never publish passwords, private keys or Wazuh enrollment secrets.
- Check screenshots for sensitive information before adding them to a public repository.

As I continue the lab, I'll record the VMware network mode, where the Wazuh components are running, and which Windows event channels are configured for collection.
