# Deployment Notes

These are my notes from setting up the virtual lab. I keep the steps I verified separate from checks I have not completed yet.

## 1. Ubuntu Server

I created an Ubuntu Server 24.04.1 LTS VM in VMware Workstation, installed the operating system, and configured a local account.

To check the current guest address from Ubuntu:

```bash
ip -br addr
```

## 2. SSH from Windows PowerShell

I connected to Ubuntu from PowerShell using SSH:

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

The session reached the Ubuntu welcome message and shell prompt. That confirmed SSH remote shell access was working during the test.

If I need to troubleshoot it later, these checks may help:

```bash
sudo systemctl status ssh
sudo ss -lntp | grep ':22'
```

These are troubleshooting commands; I'm not claiming I captured their output as part of the original successful connection.

## 3. Windows 10 VM

I created a Windows 10 VM and checked that its desktop started.

I also opened Remote Desktop Connection and reached the Windows credentials prompt. I haven't recorded a successful interactive remote desktop session yet, so RDP remains unverified.

## 4. Wazuh dashboard and Windows agent

I accessed the Wazuh dashboard and deployed the Windows agent using the dashboard's agent deployment workflow. My screenshots show:

- The Windows agent installation command being run in an elevated PowerShell window.
- The message **“The Wazuh service was started successfully.”**
- A TCP connectivity test returning `TcpTestSucceeded: True` for the port tested in the screenshot.
- Agent ID `001`, named `wazuhwindows10`, listed as **Active** in Wazuh.

The details and evidence are in [Wazuh Agent Deployment](WAZUH-AGENT-DEPLOYMENT.md).

## 5. What I still need to test

- [ ] Confirm an interactive RDP session opens and can be controlled.
- [ ] Generate a harmless Windows event and find the matching event in Wazuh.
- [ ] Inspect a relevant alert, if one is generated, and record its rule ID and severity.
- [ ] Add the original sanitized screenshots to the repository and embed them in the relevant documentation.

The checkboxes above are next steps, not claims that the tasks have been completed.

## Safety notes

I don't put passwords, private keys, or generated credentials in this repository. I also avoid exposing SSH, RDP, or the Wazuh dashboard directly to the public internet.
