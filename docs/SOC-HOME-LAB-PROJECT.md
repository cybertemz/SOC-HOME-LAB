# SOC Home Lab — Practical Deployment Documentation

## Project overview
This repository documents my hands-on SOC home lab: preparing virtual machines, configuring Windows and Ubuntu for remote administration, and deploying a Wazuh SIEM agent for endpoint monitoring practice.

The screenshots supplied for this lab are intended to provide evidence of the work completed. Each image should be kept next to the stage it supports, with any passwords, tokens, private keys, or other credentials removed before publishing.

## Lab objectives
- Prepare an isolated virtual environment using VMware Workstation.
- Start and administer a Windows 10 virtual machine.
- Connect from Windows PowerShell to an Ubuntu virtual machine using SSH.
- Practise Windows Remote Desktop (RDP) access and distinguish a credential prompt from a confirmed desktop session.
- Install/access Wazuh and deploy the Windows agent.
- Document what each test proves and identify the next validation steps.

## 1. Virtualisation and Windows 10 VM
**Purpose:** Virtual machines allow me to practise system administration and security monitoring in an isolated lab without changing my main operating system.

**Work performed:** I prepared the VMware environment and started a Windows 10 guest virtual machine.

**Evidence and verification:** A Windows desktop running inside VMware demonstrates that the guest operating system boots. It does not, by itself, prove remote connectivity or SIEM monitoring.

## 2. Ubuntu Server and SSH from Windows
**Purpose:** SSH is a standard secure method for remote Linux administration. Connecting from Windows PowerShell demonstrates host-to-guest management without relying only on the Ubuntu console.

**Work performed:** I used the Windows SSH client to connect to the Ubuntu VM using its lab username and private lab IP address.

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

**Verification:** A successful shell prompt after connecting is evidence that SSH worked at the time of the test. Check the Ubuntu VM's current address before reconnecting because virtual-network addresses can change.

## 3. Windows Remote Desktop (RDP)
**Purpose:** RDP provides graphical remote access to a Windows system and is separate from SSH.

**Work performed:** I tested the remote-access workflow from the Windows host to the Windows 10 VM.

**Verification status:** Reaching a credential prompt shows that the connection reached the authentication stage; it is not proof of a successful desktop login. Only mark this stage complete after a remote Windows desktop is visibly established.

## 4. Wazuh SIEM and Windows agent
**Purpose:** Wazuh provides security monitoring capabilities, including endpoint data collection and analysis. The agent collects relevant endpoint data and sends it to the Wazuh manager for processing.

**Work performed:** I installed/accessed the Wazuh environment and worked through deployment and connection checks for a Windows endpoint agent.

**Evidence interpretation:** A reachable dashboard confirms dashboard access. A running Windows agent service and a successful connectivity check support that the endpoint agent is running and can reach its manager. An endpoint shown as active supports agent connectivity at that time.

**Important limitation:** Agent connectivity alone does not prove that a security event was successfully generated, ingested, and turned into an alert. That should be a separate validation step.

## 5. Suggested final validation
1. Confirm the Windows agent service is running.
2. Confirm the endpoint appears active in Wazuh.
3. Generate a safe, controlled test event appropriate for the lab.
4. Verify that the event reaches Wazuh and, where expected, produces an alert.
5. Capture a clean screenshot of the result and remove sensitive information before publishing.

## Evidence status

The screenshot evidence has not yet been added to this repository. This document therefore describes the lab stages and verification criteria without displaying image links or implying that screenshots are already available. Add the selected original screenshots here after they have been uploaded and committed.

## Learning outcomes
This project helped me practise virtualisation, Linux remote administration, Windows remote-access concepts, and endpoint-agent deployment. It also reinforced the importance of distinguishing a successful installation from a fully verified monitoring pipeline.

## Next steps
- Add the final selected screenshots under `docs/images/`.
- Link each screenshot to the relevant stage above.
- Validate the Wazuh event-to-alert workflow and document the result.
- Keep the README and project notes aligned with the evidence actually present in the repository.
