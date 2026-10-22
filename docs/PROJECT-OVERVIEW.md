# SOC Home Lab — Project Overview

## What I'm working on

I'm building this lab to get a better understanding of the basics of SOC work: managing Windows and Linux machines, collecting endpoint information, and learning how to investigate events in Wazuh.

Everything runs in VMware Workstation on my Windows computer.

## My lab setup

| Component | Purpose |
|---|---|
| Windows host | Runs the virtual machines |
| VMware Workstation Pro 17 | Provides the virtual lab environment |
| Ubuntu Server 24.04.1 LTS | Linux practice and Wazuh server environment |
| Windows 10 Pro VM | Windows endpoint for monitoring |
| Windows PowerShell | Used to connect to Ubuntu over SSH |
| Wazuh | Central place to review endpoint status, events and alerts |
| Sysmon | Records detailed activity on the Windows endpoint |

## What I've done so far

### Ubuntu and SSH

I installed Ubuntu Server in VMware and set up a local account. I then connected to it from Windows PowerShell using SSH:

    ssh <ubuntu-username>@<ubuntu-lab-ip>

The session reached the Ubuntu welcome message and shell prompt, so SSH access worked during that test. I check the VM's current IP address before connecting because it can change.

### Windows VM and Remote Desktop

I created the Windows 10 virtual machine and confirmed that its desktop started. I also opened Remote Desktop Connection and reached the credentials prompt. I haven't yet confirmed a complete remote desktop session, so I still need to test that part.

### Wazuh

I accessed the Wazuh dashboard and deployed the Wazuh agent to my Windows VM. The screenshots I have show the service starting and the endpoint appearing as Active in the dashboard.

That is a useful connection check, but it does not prove that a particular event has been collected and analysed. I still need to find a specific test event in Wazuh and document what happens to it.

## Current progress

| Task | Current status |
|---|---|
| Ubuntu Server installed | Completed |
| SSH from PowerShell to Ubuntu | Tested successfully |
| Windows 10 VM created and started | Completed |
| Wazuh dashboard accessed | Completed |
| Windows agent shown as Active | Visible in the saved evidence |
| Full RDP desktop session | Not yet confirmed |
| Specific Windows event found in Wazuh | Not yet documented |
| Event-to-alert test | Not yet documented |

## What I'm learning

I'm learning not to treat one successful step as proof that the whole system works. SSH access, an active agent, event collection and a detection alert are separate things, and each needs its own check.

My next step is to generate a harmless Windows event, search for it in Wazuh, and save a screenshot of the result.
