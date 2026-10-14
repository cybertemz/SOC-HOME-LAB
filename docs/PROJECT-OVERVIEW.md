# My SOC Home Lab — Overview

## Why I'm building this

I'm using a small virtual lab to practise the basics of SOC work: managing Linux and Windows machines, connecting to systems remotely, and learning how endpoint information appears in a security-monitoring tool.

I want this repository to be a useful record of what I actually set up, what I checked, and what I still need to learn.

## My environment

| Part | Details |
|---|---|
| Host computer | Windows |
| Virtualization | VMware Workstation Pro 17 |
| Linux VM | Ubuntu Server 24.04.1 LTS |
| Windows VM | Windows 10 |
| SSH client | Windows PowerShell |
| Monitoring platform | Wazuh |

## Work I've completed

### Ubuntu Server

I installed Ubuntu Server in VMware and configured a local account during setup.

### SSH from PowerShell

I connected to the Ubuntu VM from Windows PowerShell using SSH. The session reached the Ubuntu welcome message and shell prompt, so I was able to access the Linux machine remotely.

Example command format:

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

I use the current VM address when connecting because a DHCP address can change.

### Windows 10 VM

I created a Windows 10 virtual machine and checked that the desktop started. I also tried the Remote Desktop Connection workflow, but my notes only confirm that it reached the credentials prompt. I won't call RDP fully working until I verify an interactive desktop session.

### Wazuh and the Windows agent

I accessed the Wazuh dashboard and used its agent deployment workflow for my Windows VM. My screenshots show the Wazuh service starting successfully, a successful TCP connectivity test, and the endpoint listed as Active with agent ID `001` and name `wazuhwindows10`.

That confirms the agent deployment status shown in those screenshots. I still need a separate test showing a specific Windows event arriving in Wazuh before I can say that event collection and detection have been validated end to end.

## Current status

| Task | Status |
|---|---|
| Ubuntu Server installed | Done |
| SSH from PowerShell to Ubuntu | Verified |
| Windows 10 VM created and started | Done |
| Wazuh dashboard accessed | Done |
| Windows Wazuh agent listed as Active | Shown in screenshots |
| RDP interactive session | Not yet confirmed |
| Specific Windows event found in Wazuh | Not yet documented |
| Event-to-alert test | Not yet documented |

## What I'm learning

I'm learning to check one part at a time instead of assuming that one successful step means the whole setup is working. For example, an Active agent is a good sign, but it's different from proving that a particular event was collected and triggered a detection.

## Next step

My next exercise is to create a harmless Windows event, search for it in Wazuh, and save the evidence. I'll update this page when I've run that test.
